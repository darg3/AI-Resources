# AI Resources

## 1) Claude Code Course by DeepLearning.AI

The definitive course on Claude Code, created with @AnthropicAI and taught by Elie Schoppik @eschoppik. If you want to use highly agentic coding - where AI works autonomously for many minutes or longer, not just completing code snippets - this is it.

This comprehensive course covers everything from fundamentals to advanced patterns.

After this short course, you'll be able to:
- Orchestrate multiple Claude subagents to work on different parts of your codebase simultaneously
- Tag Claude in GitHub issues and have it autonomously create, review, and merge pull requests
- Transform messy Jupyter notebooks into clean, production-ready dashboards
- Use MCP tools like Playwright so Claude can see what's wrong with your UI and fix it autonomously

**https://www.deeplearning.ai/short-courses/claude-code-a-highly-agentic-coding-assistant/**

## 2) Claude Code for Product Managers

https://ccforpms.com/

Source Repository: github.com/carlvellotti/claude-code-pm-course

## 3) How to Start a Project in Claude Code

Claude Code prompts:
1. Open Claude Code
2. Dump everything about your work—your work/role, tools you touch daily, tasks you repeat, stuff that annoys you, wild ideas you've always wanted to try, your passions, your hobbies, etc
3. Paste this:

   > "Based on what I shared, ask me 5-7 questions to understand my workflow better. Then suggest 3 things I could build, ranked by impact vs complexity. Use the AskUserQuestion tool to help me"

4. Answer honestly (specifics = better suggestions)
5. Pick the one that makes you go "wait, that's possible?"

Source: @krispuckett

## 4) [Placeholder - Original content missing]

## 5) Understanding Deep Learning Book

https://udlbook.github.io/udlbook/

## 6) Paper: Epistemic Diversity and Knowledge Collapse in Large Language Models

https://arxiv.org/abs/2510.04226v5

**Main results:**
- Larger models are consistently less diverse than smaller ones but also than basic web search
- Retrieval-augmented generation (RAG) significantly improves diversity, though unevenly across cultural contexts
- LLMs disproportionately reflect English-language knowledge underrepresenting local perspectives
- Researchers see improvements in diversity

## 7) Algorithms Book

https://jeffe.cs.illinois.edu/teaching/algorithms/

## 8) Vibe Coding Stack

OpenCode + the "Oh My OpenCode" plugin. It is a multi-agent setup that utilizes Opus 4.5 as an orchestrator that delegates tasks to other models best suited for the job:

- **Opus 4.5** - main driver + delegator
- **GPT 5.2** - architecture & code review
- **Sonnet 4.5** - context-efficient docs lookup
- **Grok Code** - fast codebase exploration
- **Gemini 3 Pro** - frontend UI/UX work
- **Gemini 3 Flash** - writing docs & file analysis

## 9) [Placeholder - Original content missing]

## 10) VS Code + Google Colab Integration

VS Code now connects directly to Google Colab. You get a free T4 GPU inside your editor.

https://colab.research.google.com/

## 11) Robotics Learning Roadmap

https://github.com/mithi/robotics-coursework

## 12) CAD and 3D Design Learning

- Learn Fusion 360: https://www.autodesk.com/products/fusion-360/choose-usage
- CAD course: sendcutsend.com

## 13) What is Inference?

The process where a trained AI model uses its learned knowledge to make predictions or decisions based on new data. It is the operational phase that follows training, allowing the model to make real-world predictions.

## 14) Three.js Skills for Claude Code

Create 3D Web Design Elements

https://github.com/CloudAI-X/threejs-skills

## 15) Private Lesson: Claude Cowork & Claude Code

Video with Boris Cherny, the creator of Claude

https://www.youtube.com/watch?v=DW4a1Cm8nG4

## 16) Andrej Karpathy's GitHub

https://github.com/karpathy

## 17) Budget VPS Setup with Hetzner and Tailscale

Go to http://hetzner.com

1. Set up a $2.50/mo VPS
2. Add SSH key when creating
3. Login, first install Tailscale on VPS and laptop
4. Once it works, add the Tailscale subnet (google the address) to Hetzner inbound firewall SSH port, don't add any more inbound ports
5. Now only you can SSH into it - safe!
6. Then install OpenClaw on the VPS via SSH
7. Don't connect any of your accounts, make a Telegram bot and add that
8. Then play with it!

Source: @levelsio

## 18) [Placeholder - Original content missing]

## 19) How /learn Works in Claude Code

When you use /learn three.js in Claude Code, here's what happens step-by-step:

### 1. Skill Creation Process Begins

I recognize that you want to teach me about Three.js, and I start creating a structured skill file.

### 2. I Generate a SKILL.md File

I create a markdown file at /mnt/skills/user/three.js/SKILL.md that contains:

- **Description:** What this skill is for (Three.js development best practices)
- **Guidelines:** Specific instructions on how to use Three.js effectively
- **Common patterns:** Code examples, best practices, gotchas to avoid
- **Use cases:** When and how to apply this knowledge

### 3. Content Gathering

I'll likely use web search to gather current, accurate information about:

- Latest Three.js best practices
- Common pitfalls and how to avoid them
- Performance optimization tips
- Recommended patterns and anti-patterns
- Version-specific information

### 4. Skill Becomes Available

Once created, this skill is stored persistently and shows up in my <available_skills> list that I can see at the start of each conversation.

### 5. Future Use

In future conversations, when you ask me to do anything related to 3D graphics or Three.js:

- I'll automatically recognize that my three.js skill is relevant
- I'll use the view tool to read /mnt/skills/user/three.js/SKILL.md
- I'll follow the guidelines and best practices documented there
- My responses will be informed by the specialized knowledge in that skill

## 20) Workflow Orchestration & Task Management

### Workflow Orchestration

#### 1. Plan Mode Default
- Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)
- If something goes sideways, STOP and re-plan immediately — don't keep pushing
- Use plan mode for verification steps, not just building
- Write detailed specs upfront to reduce ambiguity

#### 2. Subagent Strategy
- Use subagents liberally to keep main context window clean
- Offload research, exploration, and parallel analysis to subagents
- For complex problems, throw more compute at it via subagents
- One task per subagent for focused execution

#### 3. Self-Improvement Loop
- After ANY correction from the user: update `tasks/lessons.md` with the pattern
- Write rules for yourself that prevent the same mistake
- Ruthlessly iterate on these lessons until mistake rate drops
- Review lessons at session start for relevant project

#### 4. Verification Before Done
- Never mark a task complete without proving it works
- Diff your behavior between main and your changes when relevant
- Ask yourself: "Would a staff engineer approve this?"
- Run tests, check logs, demonstrate correctness

#### 5. Demand Elegance (Balanced)
- For non-trivial changes: pause and ask "is there a more elegant way?"
- If a fix feels hacky: "Knowing everything I know now, implement the elegant solution"
- Skip this for simple, obvious fixes — don't over-engineer
- Challenge your own work before presenting it

#### 6. Autonomous Bug Fixing
- When given a bug report: just fix it. Don't ask for hand-holding
- Point at logs, errors, failing tests — then resolve them
- Zero context switching required from the user
- Go fix failing CI tests without being told how

### Task Management

1. **Plan First:** Write plan to `tasks/todo.md` with checkable items
2. **Verify Plan:** Check in before starting implementation
3. **Track Progress:** Mark items complete as you go
4. **Explain Changes:** High-level summary at each step
5. **Document Results:** Add review section to `tasks/todo.md`
6. **Capture Lessons:** Update `tasks/lessons.md` after corrections

### Core Principles
- **Simplicity First:** Make every change as simple as possible. Impact minimal code.
- **No Laziness:** Find root causes. No temporary fixes. Senior developer standards.
- **Minimal Impact:** Changes should only touch what's necessary. Avoid introducing bugs.

Source: @promptcowboy on X

## 21) Vibecoders Guide to the Galaxy

Interesting guidelines and tips for vibecoding

https://www.linkedin.com/pulse/everything-can-misunderstood-vibecoders-guide-galaxy-amarie-pe3hf

## 22) Clone Wars - 100+ Open-Source Clones

Popular sites like Airbnb, Amazon, Instagram, Netflix, Tiktok, Spotify, Whatsapp, Youtube, etc. See source code, demo links, and tech stacks.

https://github.com/GorvGoyl/Clone-Wars

## 23) Greenlight - Apple App Store Compliance Scanner

Pre-submission compliance scanner for the Apple App Store

https://github.com/RevylAI/greenlight

## 24) Design, Color Palette, UI/UX Design

https://colorpalette.pro

## 25) [Placeholder - Original content missing]

## 26) The Complete Guide to Building Skills for Claude

https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf?hsLang=en

## 27) Voice: NVIDIA PersonaPlex 7b v1

https://huggingface.co/nvidia/personaplex-7b-v1

## 28) Claude Code Security

https://www.anthropic.com/news/claude-code-security

Static analysis—a widely deployed form of automated security testing—is typically recommended for security best practices.

## 29) Generate Unit & E2E Tests with 100% Coverage

Ask Codex to generate unit & e2e tests with 100% coverage. This literally turns your vibe-coded half-baked project into a full-blown production-ready product.

In addition, ask it to conduct a serious security audit and fix all issues. Make sure to connect Stripe/Vercel/Supabase MCPs, so that it also checks all the settings there - that's where most of the security holes are (e.g., inside Supabase).

## 30) ContextPlus - Context Bloat Reducer

An open-source solution to context bloat. An agent using this tool used ~6.5k fewer tokens.

https://contextplus.vercel.app/

## 31) LLMFit - Right-Size LLM Models

A terminal tool that right-sizes LLM models to your system's RAM, CPU, and GPU. Detects your hardware, scores each model.

https://github.com/AlexsJones/llmfit

## 32) Machine Learning Systems Book

Principles and Practices of Engineering Artificially Intelligent Systems

https://github.com/harvard-edge/cs249r_book

## 33) NotebookLM

Upload PDFs, websites, YouTube videos, audio files, Google Docs, Google Slides and more. NotebookLM will summarize them and make interesting connections between them.

https://notebooklm.google/

## 34) The Complete Guide to Building Skills for Claude

https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf?hsLang=en

## 35) Seetrance 2.0 - Video Generation Tool

Very realistic video generation tool

https://seed.bytedance.com/en/seedance2_0

## 36) Stanford CS336 - Language Modeling from Scratch

Free course on YouTube by Percy Liang where you build an LLM.

https://www.youtube.com/watch?v=SQ3fZ1sAqXI&list=PLoROMvodv4rOY23Y0BoGoBGgQ1zmU_MT_

Check prerequisites: https://cs336.stanford.edu/

## 37) Digital Design and Computer Architecture

L1: Intro: Fundamentals, Transistors, Gates (Spring 2025)

https://www.youtube.com/watch?v=ubhxKNlOlRg&list=PL5Q2soXY2Zi9Eo29LMgKVcaydS7V1zZW3

## 38) Paperclip - AI Employee Automation

Hire AI employees, set goals, automate jobs and your business runs itself.

https://paperclip.ing/

Source: https://github.com/paperclipai/paperclip

## 39) Insanely Fast Whisper

An opinionated CLI to transcribe audio files. Transcribe 150 minutes (2.5 hours) of audio efficiently.

https://github.com/Vaibhavs10/insanely-fast-whisper

## 40) The Ultimate Guide to Grok Imagine Videos

https://x.com/XCreators/status/2037642851732066580

## 41) Claude Code Source Code Leak & NPM Supply Chain Security

Claude Code source code was leaked due to an npm account hijack.

Reference: https://github.com/instructkr/claw-code

**Important npm security practices:**

- Make sure you always commit your project with the package-lock.json file. It is the ONLY version locking enforcement mechanism.
- Use `npm ci` instead of `npm install`. The first one will work ONLY if package-lock.json exists.
- If you need to update or pull new packages, use the `--min-release-age` flag (available since npm v11.10.0) to make sure you only install updates which are at least 7 days old:

  ```bash
  npm install --min-release-age=7
  ```

  Or hardcode this setting into your .npmrc file:

  ```
  min-release-age=7
  ```

- There will be more malicious updates to popular npm packages in the future, driven by supply chain attacks. It's just the beginning. Hopefully, they will be caught in the first 24 hours.

## 42) GStack - AI-Powered Engineering Team

An eng manager who locks architecture. A designer who catches AI slop. A QA lead who opens a real browser and clicks through your app. A security officer who runs OWASP audits. A release engineer who ships the PR.

23 specialists. 8 power tools. All Markdown files. All free.

Garry Tan built this while running Y Combinator full-time. He's been shipping 10,000 to 20,000 lines of production code per day. Part-time. In the last 60 days: 600,000+ lines of production code.

**Here's what you get:**

- `→ /office-hours` runs a YC-style founder session that reframes your product before you write a single line of code
- `→ /plan-ceo-review` rethinks your feature and finds the 10-star product hiding inside it
- `→ /plan-eng-review` generates architecture diagrams, data flow, edge cases, and a full test matrix
- `→ /review` does staff-engineer-level code review and auto-fixes obvious bugs on the spot
- `→ /qa` opens a real Chromium browser, clicks through your staging app, finds bugs, writes regression tests, and verifies the fixes
- `→ /cso` runs OWASP Top 10 and STRIDE threat models with zero false-positive noise
- `→ /ship` syncs main, runs tests, audits coverage, pushes, and opens the PR in one command
- `→ /browse` gives your agent a persistent browser with sub-100ms latency per command
- `→ /design-shotgun` generates multiple design variants and opens a comparison board in your browser
- `→ /retro` runs a team-aware weekly retro with per-person breakdowns and shipping streaks
- `→ /codex` gets a second opinion from OpenAI's Codex CLI so two different AIs review the same diff
- `→ /careful` and `→ /freeze` add safety guardrails that warn before destructive commands like rm -rf or DROP TABLE

Source: @Meer_AIIT

## 43) Mesh-LLM - Pool Compute for Open Models

Pool compute to run open models. Built by @michaelneale at Block.

https://docs.anarchai.org

## 44) Andrej Karpathy Skills for Claude Code

A single CLAUDE.md file to improve Claude Code behavior, derived from Andrej Karpathy's principles.

https://github.com/forrestchang/andrej-karpathy-skills

## 45) Bonsai 8B - First Commercially Viable 1-bit LLMs

https://prismml.com/news/bonsai-8b

HuggingFace: https://huggingface.co/prism-ml/Bonsai-8B-gguf

## 46) Vibe Coding in Production - Masterclass from Anthropic

Code w/ Claude: https://www.youtube.com/watch?v=fHWFF_pnqDk

## 47) A Masterclass in Using LLM in Day to Day Tasks

By Andrej Karpathy

https://www.youtube.com/watch?v=EWvNQjAaOHw

## 48) NotebookLM is an AI-powered research and note-taking tool developed by Google. It assists users in summarizing and interacting with their documents, making it a valuable resource for students, researchers, and professionals.

can create audio/ podcast style summary

https://notebooklm.google/

## 49) Unlimited OCR Model - entire book in a single pass

https://huggingface.co/baidu/Unlimited-OCR

## 50) How Loops Work - Claude Code 

https://claude.com/blog/getting-started-with-loops

## 51) Aval - open-source format for interactive video on the web

https://github.com/pixel-point/aval

## 52) Kimi K3 launched - open-weight model and said the full model weights will be released by July 27, 2026

https://platform.kimi.ai/docs/guide/kimi-k3-quickstart
https://www.kimi.com/en
