# Spending Tokens Like They're Yours

A practical guide to keeping context small, sessions sharp, and token bills low — built for engineers onboarding to Claude Code, and tuned for veterans who want to min–max every window.

**Onboarding + Optimization | Sources: Anthropic Docs, A. Karpathy, Production Teams**

---

## The one idea everything hangs on

Almost every tip in this guide is downstream of a single constraint that Anthropic states plainly in its own documentation: **Claude's context window fills up fast, and quality degrades as it fills.**[^1] The window holds your entire conversation — every message, every file Claude reads, every command output — and a single debugging session can burn tens of thousands of tokens. As it gets full, Claude starts "forgetting" earlier instructions and making more mistakes.[^1]

Three properties of the context window are worth internalizing early. It is **finite** (there is a hard token ceiling), it **degrades** (accuracy drops as it fills with noise), and **attention is a limited resource** (the instinct to dump in information "just in case" backfires — important details get buried and accuracy falls).[^1] Tokens are also money: across enterprise deployments Anthropic reports an average of roughly **$13 per developer per active day**, with most users staying under $30.[^2] Cutting wasted context cuts both error rate and cost at the same time.

Andrej Karpathy gave this discipline its name. He frames *context engineering* as the craft of loading the window with exactly the right information for the next step — no more, no less.[^5] That is the lens for everything below. For each practice you get the principle, why it works, a real-world example, and a **min–max** note for senior engineers.

---

## 01 Session hygiene: clear, compact, rewind

### Use `/clear` between unrelated tasks

**Why it works:** Stale context isn't free. Every message you send re-sends the whole conversation, so leftover files and dead-end discussion from a finished task get billed on *every* subsequent turn and dilute Claude's attention.[^2] `/clear` resets the window entirely so the next task starts clean.[^1]

> **Real-world example · the "kitchen sink" session**
> 
> Anthropic lists this as a top failure pattern: you start with one task, ask Claude something unrelated, then circle back to the first — and now the window is full of irrelevant information. Their prescribed fix is literally one command: `/clear` between unrelated tasks.[^1] A related trap is the *correction spiral* — if you've corrected Claude more than twice on the same issue, the context is polluted with failed approaches. Clear it and restart with a sharper prompt that bakes in what you learned.[^1]

### Don't use the latest most powerful model for a small task

**Why it works:** Opus costs roughly **5× more per token than Sonnet**, and on subscription plans it burns through your quota window faster.[^8] Using Opus to rename a variable, format code, or run a simple grep is like using a supercomputer to count coins — technically correct but economically absurd. Match the model to the actual reasoning load.[^8]

The heuristic is simple: Sonnet handles the vast majority of coding tasks well. Reserve Opus for genuinely hard decisions (cross-system architectural reasoning, complex multi-file refactoring, or untangling gnarly bugs). Drop to Haiku for trivial, repetitive work (formatting, search-and-replace, linting).[^2] Switch mid-session with `/model sonnet` or `/model haiku` rather than locking into one for the whole session.

> **Real-world example · the cost math**
>
> A junior engineer spent 3 days in Opus "because I wasn't sure what I was doing," burning tokens on basic file exploration and variable renaming. Sonnet would have handled all of it fine; the context was small and the decisions were straightforward. Switching to Sonnet for the same work on the next project cut costs roughly **80%** for the same output quality.[^8] Opus is a tool to reach for, not a default.

> **Min–max for seniors**
>
> Use the `opusplan` model alias: it plans with Opus (where reasoning quality matters most) and auto-switches to Sonnet for code generation — Opus-grade thinking without paying Opus rates for every line. For team workflows, make `/model sonnet` your session default and document when Opus is worth invoking (e.g., "before major architectural changes"). Track which decisions actually needed deep reasoning and which didn't; you'll train an intuition for when to switch.[^2]

### Reach for `/compact` when the thread still matters

When you need continuity but the window is getting heavy, `/compact` summarizes history while preserving code and key decisions. Steer it: `/compact Focus on the API changes` tells Claude what to keep.[^2] You can bake the same instruction into `CLAUDE.md` so critical context always survives summarization.[^1]

> **Min–max for seniors**
>
> Run `/usage` or wire context-window usage into your `statusline` so you can see the window filling in real time rather than discovering it at the compaction warning.[^2] Use `/rename` before a `/clear` so the session is easy to `/resume` later, and treat `Esc·Esc` / `/rewind` checkpoints as cheap experiments — try the risky approach, rewind if it fails, instead of arguing with a polluted context.[^1]

---

## 02 Treat `CLAUDE.md` like code, not a wiki

`CLAUDE.md` loads into context at the start of *every* session, so every line is a tax you pay on all work, relevant or not.[^2] The goal is a short, high-signal file. Anthropic's test for each line: *"Would removing this cause Claude to make mistakes?"* If not, cut it.[^1]

| Include | Exclude |
|---------|---------|
| Bash commands Claude can't guess; required env vars | Anything Claude can learn by reading the code |
| Code-style rules that differ from defaults | Standard language conventions Claude already knows |
| Test runners, repo etiquette, branch naming | Detailed API docs (link out instead) |
| Project-specific architecture decisions, gotchas | File-by-file descriptions; "write clean code" |

> **Real-world example · the bloated memory file**
>
> Anthropic's guidance is blunt: if your `CLAUDE.md` is too long, Claude ignores half of it because the important rules get lost in the noise. The tell is behavioral — "if Claude keeps doing something you have a rule against, the file is probably too long and the rule is getting lost."[^1] The fix is to prune ruthlessly and aim to keep the file under ~200 lines, moving specialized, occasional instructions (PR-review steps, migration playbooks) into on-demand **Skills** that load only when invoked.[^2]

> **Min–max for seniors**
>
> Move workflow-specific instructions out of `CLAUDE.md` and into `.claude/skills/`. A skill costs zero tokens until Claude actually needs it, which keeps the base context of every unrelated session smaller. Check `CLAUDE.md` into git, review it when things go wrong, and prune it on a schedule the way you'd refactor dead code.[^1]

---

## 03 Explore → plan → code (don't skip the middle)

Letting Claude jump straight to coding produces code that solves the wrong problem — and re-work is the most expensive way to spend tokens. Plan mode separates exploration from execution: Claude reads files and proposes an approach for your approval before touching anything.[^1,^2]

The math is the real argument. If each unguided decision is ~80% right, a feature with 20 such decisions has roughly a **0.8^20 ≈ 1%** chance of being fully correct. Planning collapses those ambiguous calls into a reviewed spec where each one is settled up front.[^7] It's consistent with Anthropic's own finding that unguided attempts succeed only about a third of the time.[^7]

> **Real-world example · the plan.md annotation cycle**
>
> Engineer Boris Tane's documented workflow, cited in DataCamp's write-up of production-team practices, runs like this: have Claude draft a `plan.md`, open it in your editor, and annotate inline wherever Claude made the wrong call — e.g. *"use `drizzle:generate`, not raw SQL"* or *"this should be `PATCH`, not `PUT`."* Send it back with the guard phrase **"address all notes, don't implement yet"** and repeat until the plan has no ambiguity left. Only then does Claude implement — with far fewer wrong turns, because every decision is already made.[^7]

> **Min–max for seniors**
>
> Skip planning when you could describe the diff in one sentence (a typo, a log line, a rename) — plan mode has overhead too.[^1] For genuinely large features, have Claude *interview you* first using its question tool, write the result to `SPEC.md`, then execute in a **fresh session** so implementation runs on clean context against a written spec.[^1]

---

## 04 Write specific prompts to prevent blind scanning

Vague requests trigger broad, expensive scanning. The more precise the instruction, the fewer files Claude reads and the fewer corrections you pay for downstream.[^2]

> **Real-world example · before / after, from the docs**
>
> Anthropic contrasts these directly:
>
> **Vague (scans widely):** "fix the login bug"
>
> **Specific (works surgically):** "users report login fails after session timeout. check the auth flow in `src/auth/`, especially token refresh. write a failing test that reproduces it, then fix it"
>
> The "after" prompts name the file, the scenario, and what "fixed" looks like — so Claude doesn't read half the repo to infer them.[^1]

> **Min–max for seniors**
>
> Always hand Claude a way to *verify* its own work — test cases, an expected output, a screenshot to diff against. A check it can read closes the loop without you in it, and catches the "plausible but wrong" implementation before you spend tokens requesting fixes.[^1,^2]

---

## 05 Offload heavy work off the main context

### Pre-filter verbose output with hooks

Hooks run scripts at fixed points in Claude's loop and can shrink data *before* Claude ever sees it.[^2]

> **Real-world example · the log-filtering hook**
>
> Anthropic's own example: instead of letting Claude read a 10,000-line log file to find errors, a `PreToolUse` hook greps for failures and returns only the matching lines — cutting context for that step from tens of thousands of tokens down to hundreds.[^2]
>
> ```bash
> # filter test output to failures only
> $cmd 2>&1 | grep -A 5 -E '(FAIL|ERROR|error:)' | head -100
> ```

### Delegate investigation to subagents

When Claude researches a codebase it reads many files — all of which land in your window. Subagents run in a *separate* context and report back only a summary.[^1]

> **Real-world example · scoped investigation**
>
> A prompt like *"use subagents to investigate how our auth system handles token refresh, and whether we have OAuth utilities to reuse"* sends the file-reading into an isolated window; your main conversation receives findings, not hundreds of files.[^1] The same pattern works for a fresh-context review of a diff.
>
> *Caveat:* multi-agent teams aren't free — Anthropic notes teammates each carry their own window and can use roughly **7×** the tokens of a standard session, so keep teams small and tasks self-contained.[^2]

> **Min–max for seniors**
>
> Push specialized knowledge into a **Skill** (e.g. a "codebase-overview" skill describing architecture and conventions) so Claude gets the map instantly instead of spending tokens reading files to reconstruct it.[^2]

---

## 06 Match the model — and trim the tooling

### Don't run your most expensive model by default

Sonnet handles most coding tasks well and costs far less than Opus — on API billing, Opus runs about **5×** the per-token cost of Sonnet, and on subscription plans heavier models drain your quota window faster.[^8] Reserve Opus for genuinely hard reasoning; drop to Haiku for trivial, repetitive work.[^2]

> **Real-world example · opusplan**
>
> A common production setup: start sessions on Sonnet and switch to Opus only for gnarly cross-system debugging. Better still, the `opusplan` alias plans with Opus (where reasoning quality matters most) and auto-switches to Sonnet for the actual code generation — Opus-grade thinking without paying Opus rates per line.[^8]

### Keep MCP overhead off the window

- **Prefer CLI tools** like `gh`, `aws`, and `gcloud` over equivalent MCP servers — they add no per-tool listing to context and Claude runs them directly.[^2]
- **Disable unused servers** with `/mcp`, and run `/context` to see exactly what's consuming space.[^2]
- **Tune extended thinking** down for simple tasks — thinking tokens bill as output, so lower the effort level (or `MAX_THINKING_TOKENS`) when deep reasoning isn't needed.[^2]

---

## 07 Stop re-explaining: the durable-memory pattern

The most expensive habit isn't a long session — it's rebuilding context from scratch every time one ends. Karpathy's answer is to treat the model less like a disposable chat partner and more like a research librarian that maintains a living set of Markdown files.[^4]

His "LLM Knowledge Base" pattern is a simple, file-first pipeline: immutable `raw/` source documents are *compiled* by the LLM into a continuously-updated `wiki/` of Markdown, which in turn informs the `code/` you generate. The rule of thumb from practitioners building on it: under roughly 80k tokens of notes, the model just reads the Markdown directly — no vector database or RAG pipeline needed.[^4,^9] Markdown is the connective tissue throughout because it's compact, diff-able, and easy for the model to parse.[^9]

> **Real-world example · 95% fewer tokens**
>
> In one reported case, a user compiled **383 files and 100+ meeting transcripts** into a compact Markdown wiki using Karpathy's raw→wiki pattern and cut Claude token usage by about **95%** — because the model reads a curated, compressed knowledge base instead of re-ingesting raw source material on every question.[^9]

The practical takeaway for a coding workflow: commit frequently, dump decisions and progress into Markdown (`plan.md`, `SPEC.md`, a project wiki), and treat every session as disposable. Never let a long-running session be your only record of what you've decided — that's exactly the state that forces a costly context rebuild after a `/clear` or a timeout.[^7]

> **Min–max for seniors**
>
> Make write-back mandatory: every architectural decision goes into the wiki as you make it. The payoff compounds — the next session, the next teammate, and the next subagent all start from compressed, high-signal Markdown instead of paying to rediscover it.[^4,^9]

---

## 08 The anti-pattern cheat sheet

Anthropic's five most common token sinks — learn to spot them early.[^1]

| Failure pattern | Fix |
|-----------------|-----|
| Kitchen-sink session | `/clear` between unrelated tasks. |
| Correcting over and over | After two failed corrections, `/clear` and write a better initial prompt. |
| Over-specified CLAUDE.md | Prune ruthlessly; move occasional instructions to Skills. |
| Trust-then-verify gap | Always provide a check (tests, scripts, screenshots). If you can't verify it, don't ship it. |
| Infinite exploration | Scope investigations narrowly, or hand them to subagents. |

One closing caveat from Anthropic worth keeping in mind: these are defaults, not laws. Sometimes you *should* let context accumulate because you're deep in one complex problem and the history is genuinely valuable; sometimes a vague prompt is exactly right because you want to see how Claude frames a problem before you constrain it. Pay attention to what works in your own sessions — that intuition is the real skill.[^1]

---

## Notes & sources

[^1]: Anthropic, *Best practices for Claude Code*. code.claude.com/docs/en/best-practices — context window as the fundamental constraint; `/clear`, `/compact`, plan mode, subagents, CLAUDE.md guidance, and the common failure patterns.

[^2]: Anthropic, *Manage costs effectively*. code.claude.com/docs/en/costs — reduce-token-usage strategies: context management, model selection, MCP overhead, hooks/skills, extended thinking, subagent and agent-team costs, per-developer cost figures.

[^3]: Anthropic, *Claude prompting best practices*. platform.claude.com/docs — general guidance on token budgets and saving state before context refreshes.

[^4]: A. Karpathy, *"LLM Knowledge Bases"* workflow (April 2026), as reported by VentureBeat and others — LLM-maintained Markdown wiki as a file-first alternative to RAG; raw→wiki→code pipeline. (Primary material is an X post and a public GitHub gist; cited here via secondary coverage.)

[^5]: A. Karpathy — origin of the term *context engineering*, framed as filling the context window with the right information for the next step (paraphrased).

[^6]: B. Tane, *"How I use Claude Code"* — the `plan.md` annotation cycle and the "address all notes, don't implement yet" guard phrase.

[^7]: DataCamp, *Claude Code Best Practices: Planning, Context Transfer, TDD* (Mar 2026) — production-team practices (Abnormal AI, incident.io, Trail of Bits), the compounding-error argument for planning, Anthropic's ~33% unguided success rate, and the Boris Tane annotation cycle.

[^8]: KDnuggets, *7 Practical Ways to Reduce Claude Code Token Usage* (May 2026) — model-selection economics (Opus ~5× Sonnet) and the `opusplan` hybrid.

[^9]: MindStudio, coverage of Karpathy's LLM wiki pattern (Apr–May 2026) — Markdown-first knowledge base; the reported 383-file / 100-transcript case with ~95% token reduction; the ~80k-token "read directly" threshold.

---

**Compiled May 2026.** Product commands and figures reflect Claude Code documentation current at that time; verify against the live docs as the tool evolves. This guide paraphrases its sources and is not affiliated with or endorsed by the cited authors.
