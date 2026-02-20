1) The definitive course on Claude Code, created with @AnthropicAI
 and taught by Elie Schoppik @eschoppik
. If you want to use highly agentic coding - where AI works autonomously for many minutes or longer, not just completing code snippets - this is it.

 This comprehensive course covers everything from fundamentals to advanced patterns.

After this short course, you'll be able to:
- Orchestrate multiple Claude subagents to work on different parts of your codebase simultaneously
- Tag Claude in GitHub issues and have it autonomously create, review, and merge pull requests
- Transform messy Jupyter notebooks into clean, production-ready dashboards
- Use MCP tools like Playwright so Claude can see what's wrong with your UI and fix it autonomously

 ** https://www.deeplearning.ai/short-courses/claude-code-a-highly-agentic-coding-assistant/**

 2) Claude Code for Product Managers - https://ccforpms.com/ + Source Repository: github.com/carlvellotti/claude-code-pm-course
 3) How to a project in Claude Code (Claude Code prompts)
         1. Open Claude Code
         2. Dump everything about your work—your work/role, tools you touch daily, tasks you repeat, stuff that annoys you, wild ideas you've always wanted to try, your passions, your hobbies, etc
         3. Paste this:
        "Based on what I shared, ask me 5-7 questions to understand my workflow better. Then suggest 3 things I could build, ranked by impact vs complexity. Use the AskUserQuestion tool to help me"
         Answer honestly (specifics = better suggestions)
         4. Pick the one that makes you go "wait, that's possible?"
    source: @krispuckett

5) Understanding Deep Learning Book - https://udlbook.github.io/udlbook/


6) Paper - Epistemic Diversity and Knowledge Collapse in Large Language Models - https://arxiv.org/abs/2510.04226v5
    Here the main results :
      - Larger models are consistently less diverse than smaller ones but also 
        than basic web search (cf. 2nd picture)
      - Retrieval-augmented generation (RAG) significantly improves diversity, though unevenly across cultural contexts
      - LLMs disproportionately reflect English-language knowledge underrepresenting local perspectives (cf. 3rd picture)
    - Researchers see improvements in diversity


7) Algorithms book - https://jeffe.cs.illinois.edu/teaching/algorithms/

8) Vibe coding stack:

    OpenCode + the "Oh My OpenCode" plugin. 

    It is a multi-agent setup that utilizes Opus 4.5 as an orchestrator that delegates tasks to other models best suited         for the job:

    · Opus 4.5 - main driver + delegator
    · GPT 5.2 - architecture & code review
    · Sonnet 4.5 - context-efficient docs lookup
    · Grok Code - fast codebase exploration
    · Gemini 3 Pro -  frontend UI/UX work
    · Gemini 3 Flash - writing docs & file analysis
   
10) VS Code now connects directly to Google Colab. You get a free T4 GPU inside your editor. - https://colab.research.google.com/

11) Roadmap for learning robotics - https://github.com/mithi/robotics-coursework
12) Learn Fusion 360 and then CAD - https://www.autodesk.com/products/fusion-360/choose-usage; CAD course : sendcutsend.com
13) What is inference? the process where a trained AI model uses its learned knowledge to make predictions or decisions based on new data. It is the operational phase that follows training, allowing the AI to apply what it has learned to real-world situations. Inference is when an AI model analyzes input data and generates an output, such as a prediction or classification. For example, a self-driving car uses inference to recognize a stop sign it has never encountered before.

14) Threejs Skills for Claude Code to create 3D Web Design Elements - https://github.com/CloudAI-X/threejs-skills
15) Private lesson on Claude Cowork & Claude Code video with Boris Cherny the creator of Claude - https://www.youtube.com/watch?v=DW4a1Cm8nG4
16) https://github.com/karpathy
17) Go to http://hetzner.com

    Set up a $2.50/mo VPS
    
    Add SSH key when creating
    
    Login, first install Tailscale on VPS and laptop
    
    Once it works add the Tailscale subnet (google the address) to Hetzner inbound firewall SSH port, don't add any more inbound ports
    
    Now only u can SSH into it, safe
    
    Then install OpenClaw on the VPS via SSH
    
    Don't connect any of your accounts, make a Telegram bot and add that
    Then play with it! source @levelsio
    
19) Great question! When you use /learn three.js in Claude Code, here's what happens step-by-step:
    1. Skill Creation Process Begins
    I recognize that you want to teach me about Three.js, and I start creating a structured skill file.
    2. I Generate a SKILL.md File
    I create a markdown file at /mnt/skills/user/three.js/SKILL.md that contains:
    
    Description: What this skill is for (Three.js development best practices)
    Guidelines: Specific instructions on how to use Three.js effectively
    Common patterns: Code examples, best practices, gotchas to avoid
    Use cases: When and how to apply this knowledge
    
    3. Content Gathering
    I'll likely use web search to gather current, accurate information about:
    
    Latest Three.js best practices
    Common pitfalls and how to avoid them
    Performance optimization tips
    Recommended patterns and anti-patterns
    Version-specific information
    
    4. Skill Becomes Available
    Once created, this skill is stored persistently and shows up in my <available_skills> list that I can see at the start of each conversation.
    5. Future Use
    In future conversations, when you ask me to do anything related to 3D graphics or Three.js:
    
    I'll automatically recognize that my three.js skill is relevant
    I'll use the view tool to read /mnt/skills/user/three.js/SKILL.md
    I'll follow the guidelines and best practices documented there
    My responses will be informed by the specialized knowledge in that skill

20) ## Workflow Orchestration

      ### 1. Plan Mode Default
      - Enter plan mode for ANY non-trivial task (3+ steps or architectural decisions)
      - If something goes sideways, STOP and re-plan immediately — don't keep pushing
      - Use plan mode for verification steps, not just building
      - Write detailed specs upfront to reduce ambiguity
      
      ### 2. Subagent Strategy
      - Use subagents liberally to keep main context window clean
      - Offload research, exploration, and parallel analysis to subagents
      - For complex problems, throw more compute at it via subagents
      - One task per subagent for focused execution
      
      ### 3. Self-Improvement Loop
      - After ANY correction from the user: update `tasks/lessons.md` with the pattern
      - Write rules for yourself that prevent the same mistake
      - Ruthlessly iterate on these lessons until mistake rate drops
      - Review lessons at session start for relevant project
      
      ### 4. Verification Before Done
      - Never mark a task complete without proving it works
      - Diff your behavior between main and your changes when relevant
      - Ask yourself: "Would a staff engineer approve this?"
      - Run tests, check logs, demonstrate correctness
      
      ### 5. Demand Elegance (Balanced)
      - For non-trivial changes: pause and ask "is there a more elegant way?"
      - If a fix feels hacky: "Knowing everything I know now, implement the elegant solution"
      - Skip this for simple, obvious fixes — don't over-engineer
      - Challenge your own work before presenting it
      
      ### 6. Autonomous Bug Fixing
      - When given a bug report: just fix it. Don't ask for hand-holding
      - Point at logs, errors, failing tests — then resolve them
      - Zero context switching required from the user
      - Go fix failing CI tests without being told how
      
      ## Task Management
      
      1. **Plan First**: Write plan to `tasks/todo.md` with checkable items
      2. **Verify Plan**: Check in before starting implementation
      3. **Track Progress**: Mark items complete as you go
      4. **Explain Changes**: High-level summary at each step
      5. **Document Results**: Add review section to `tasks/todo.md`
      6. **Capture Lessons**: Update `tasks/lessons.md` after corrections
      
      ## Core Principles
      - **Simplicity First**: Make every change as simple as possible. Impact minimal code.
      - **No Laziness**: Find root causes. No temporary fixes. Senior developer standards.
      - **Minimal Impact**: Changes should only touch what's necessary. Avoid introducing bugs.
      - source @promptcowboy on X

21) https://www.linkedin.com/pulse/everything-can-misunderstood-vibecoders-guide-galaxy-amarie-pe3hf - some vibecodind interesting guidelines

22) https://github.com/GorvGoyl/Clone-Wars - 100+ open-source clones of popular sites like Airbnb, Amazon, Instagram, Netflix, Tiktok, Spotify, Whatsapp, Youtube etc. See source code, demo links, tech stack, github stars.
23) https://github.com/RevylAI/greenlight - Pre-submission compliance scanner for the Apple App Store

24) Design, Color Palette, UI/UX Design - [colorpallete.pro](https://colorpalette.pro)
    
26) [https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf?hsLang=en](https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf?hsLang=en)

27) Voice NVIDIA PersonaPlex 7b v1 [https://huggingface.co/nvidia/personaplex-7b-v1](https://huggingface.co/nvidia/personaplex-7b-v1)

28) [https://www.anthropic.com/news/claude-code-security](https://www.anthropic.com/news/claude-code-security) - Static analysis—a widely deployed form of automated security testing—is typically rule-based, meaning it matches code against known vulnerability patterns. That catches common issues, like exposed passwords or outdated encryption, but often misses more complex vulnerabilities, like flaws in business logic or broken access control.
