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

Understanding Deep Learning Book - https://udlbook.github.io/udlbook/


Paper - Epistemic Diversity and Knowledge Collapse in Large Language Models - https://arxiv.org/abs/2510.04226v5
    Here the main results :
      - Larger models are consistently less diverse than smaller ones but also 
        than basic web search (cf. 2nd picture)
      - Retrieval-augmented generation (RAG) significantly improves diversity, though unevenly across cultural contexts
      - LLMs disproportionately reflect English-language knowledge underrepresenting local perspectives (cf. 3rd picture)
    - Researchers see improvements in diversity


Algorithms book - https://jeffe.cs.illinois.edu/teaching/algorithms/

Vibe coding stack:

    OpenCode + the "Oh My OpenCode" plugin. 

    It is a multi-agent setup that utilizes Opus 4.5 as an orchestrator that delegates tasks to other models best suited         for the job:

    · Opus 4.5 - main driver + delegator
    · GPT 5.2 - architecture & code review
    · Sonnet 4.5 - context-efficient docs lookup
    · Grok Code - fast codebase exploration
    · Gemini 3 Pro -  frontend UI/UX work
    · Gemini 3 Flash - writing docs & file analysis
