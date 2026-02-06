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
