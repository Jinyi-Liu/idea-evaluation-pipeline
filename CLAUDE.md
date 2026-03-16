# Idea Evaluation Pipeline - Claude Code

See `AGENTS.md` for full pipeline instructions.

## Quick Reference

This project runs a research idea evaluation pipeline for PhD students working on theory-oriented operations management, quantitative marketing, and information systems projects. The pipeline iterates through 8 steps until an idea scores >= 7/10.

### Prompt files (in project root)
- `prompt_ideas.txt` - Steps 1 and 4 (evaluate)
- `review_eval_prompt.txt` - Step 2 (review evaluation)
- `pivot_prompt.txt` - Step 3 (pivot)
- `lit_review_prompt.txt` - Step 5 (lit review, needs web search)
- `verify_lit_review_prompt.txt` - Step 6 (verify citations, needs web search + edit)
- `final_verdict_prompt.txt` - Step 7 (final verdict)
- `review_final_verdict_prompt.txt` - Step 8 (review verdict)

### Running the pipeline
1. Student creates a folder with their idea file and 3 closest papers or models.
2. Run steps sequentially, appending results to a master `.md` file.
3. Loop back to Step 3 if score < 7.
4. Use background agents for parallelizing across multiple ideas.
5. Steps 5 and 6 require web search.

### Critical
- Never fabricate citations - Steps 5 and 6 must use web search to find and verify real papers.
- Always append to the master `.md` after each step.
- Include full history when running pivot prompts.
- Evaluate for fit with `Management Science`, `MSOM`, `POM`, `Marketing Science`, and `ISR`, not finance journals.
