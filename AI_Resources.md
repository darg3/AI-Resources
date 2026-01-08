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
