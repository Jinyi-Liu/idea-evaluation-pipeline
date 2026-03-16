# Theory Research Idea Evaluation Pipeline

A structured pipeline for iteratively evaluating, pivoting, and defending theory-oriented research ideas until they reach premier operations management, quantitative marketing, or information systems journal quality.

Primary targets:
- `Management Science` (OM, Marketing, or Information Systems department, depending on the paper)
- `Manufacturing & Service Operations Management (MSOM)`
- `Production and Operations Management (POM)`
- `Marketing Science`
- `Information Systems Research (ISR)`

Designed for PhD students working on analytical, game-theoretic, optimization, dynamic, platform, or related theory papers. Works with any AI coding assistant or manually by copy-pasting prompts.

## How It Works

Your idea goes through up to 8 steps. The pipeline loops until the idea scores 7/10 or higher:

```
1. EVALUATE IDEA -> 2. REVIEW EVALUATION
                         |
                    Critique unfair? -> Re-run Step 1
                         |
                    Score >= 7? ---- Yes ----> 5. LITERATURE REVIEW
                         |                         ->
                         No                   6. VERIFY LIT REVIEW
                         ->                        ->
                    3. PIVOT IDEA           7. FINAL VERDICT
                         ->                        ->
                    4. EVALUATE PIVOT       8. REVIEW FINAL VERDICT
                         |                         |
                    Score < 7? -> Back to 3  Score >= 7? -> DONE
                    Score >= 7 -> Step 5     Score < 7  -> Back to 3
```

## Quick Start

### 1. Create your idea folder

```powershell
mkdir my_idea
```

### 2. Add your idea file

Copy `idea_template.txt` into your folder and fill it in:

```powershell
Copy-Item idea_template.txt my_idea/idea.txt
```

The template asks for:
- Research question and the substantive phenomenon
- Benchmark models and the exact theoretical departure
- Model primitives: players, timing, information, decisions, and equilibrium concept
- Main propositions or comparative statics
- Proof or tractability plan
- 3 closest papers or models with full citations, URLs, and precise differentiation
- Target journal fit and why the audience should care

The 3 closest papers are critical. Pick the models a referee would immediately cite against you, not just broadly related work. Include URLs so the pipeline can verify them.

### 3. Run the pipeline

With an AI coding tool: open this project in your tool and ask it to run the pipeline on your idea. The agent will read `AGENTS.md` (or `CLAUDE.md`) and follow the steps automatically.

Manually: copy-paste each prompt file into your preferred LLM along with the relevant input. Save each output to the correct filename. See the step-by-step guide below.

## Step-by-Step (Manual)

### Step 1: Evaluate Idea
- Prompt: `prompt_ideas.txt`
- Input: Your idea + 3 closest papers or models
- Output: Save as `my_idea/eval_my_idea_idea1.txt`
- Model: Use the strongest model available

### Step 2: Review Evaluation
- Prompt: `review_eval_prompt.txt`
- Input: Your idea + the evaluation from Step 1
- Output: Save as `my_idea/review_my_idea_idea1.txt`
- Decision: If the review finds the critique unfair, re-run Step 1 with corrections

### Step 3: Pivot Idea (if score < 7)
- Prompt: `pivot_prompt.txt`
- Input: Your idea + evaluation + review (full history)
- Output: Save as `my_idea/pivot_idea1.txt` (or `pivot_idea1_v2.txt`, `_v3.txt` if iterating)

### Step 4: Evaluate Pivot
- Prompt: `prompt_ideas.txt` (same as Step 1)
- Input: Your pivoted idea + original 3 closest papers or models
- Output: Save as `my_idea/eval_pivot_idea1.txt` (or `eval_pivot_idea1_v2.txt` if iterating)
- Decision: If score dropped or stayed flat, go back to Step 3

### Step 5: Literature Review (Threat Search)
- Prompt: `lit_review_prompt.txt`
- Input: Your pivoted idea + 3 cited papers or models
- Output: Save as `my_idea/lit_review_pivot_idea1.txt`
- Model: Use a model with web search
- Important: The prompt requires URLs for every cited paper to prevent hallucinated citations

### Step 6: Review and Verify Literature Review
- Prompt: `verify_lit_review_prompt.txt`
- Input: The lit review from Step 5
- Output: Edit the lit review file (add URLs, remove fakes) + save summary as `my_idea/review_lit_review_idea1.txt`
- Model: Must have web search access
- Important: This step catches hallucinated citations. Every paper must be verified via Google Scholar, SSRN, publisher pages, or IDEAS/RePEc.

### Step 7: Final Verdict
- Prompt: `final_verdict_prompt.txt`
- Input: Full history (all previous outputs)
- Output: Save as `my_idea/final_verdict_idea1.txt`

### Step 8: Review Final Verdict
- Prompt: `review_final_verdict_prompt.txt`
- Input: Full history + final verdict
- Output: Save as `my_idea/review_final_verdict_idea1.txt`
- Decision: If score < 7, go back to Step 3 with full history

## What Gets Scored

The evaluation is theory-first. The pipeline emphasizes:
- Novelty relative to the closest models
- Whether the new friction or mechanism actually changes insight
- Sharpness of propositions and comparative statics
- Tractability, proof burden, and credibility of the solution approach
- Managerial or substantive relevance
- Realistic fit with the target journal's audience

## Scoring Guide

| Score | Meaning | Action |
|-------|---------|--------|
| 1-3 | Low potential, mostly incremental | Major pivot or new idea needed |
| 4-6 | Moderate potential, interesting but not yet strong enough for premier OM, marketing, or IS journals | Pivot to sharpen mechanism, benchmark, and insight |
| 7-8 | Good potential, credible path to a premier field journal with refinement | Proceed carefully |
| 9-10 | Exceptional potential, unusually strong novelty and insight | Rare |

Target: 7/10 to proceed.

If an idea is stuck around 6 after multiple pivots, consider:
- Trying a different underlying phenomenon
- Narrowing the scope to one sharper mechanism
- Repositioning to a less selective journal
- Accepting that the closest models already cover most of the insight

## File Organization

```
IdeaEvaluation/
|-- README.md
|-- AGENTS.md
|-- CLAUDE.md
|-- pipeline.md
|-- prompt_ideas.txt
|-- review_eval_prompt.txt
|-- pivot_prompt.txt
|-- lit_review_prompt.txt
|-- verify_lit_review_prompt.txt
|-- final_verdict_prompt.txt
|-- review_final_verdict_prompt.txt
|-- idea_template.txt
|
`-- my_idea/
    |-- idea.txt
    |-- my_idea.md
    |-- eval_my_idea_idea1.txt
    |-- review_my_idea_idea1.txt
    |-- pivot_idea1.txt
    |-- pivot_idea1_v2.txt
    |-- eval_pivot_idea1.txt
    |-- eval_pivot_idea1_v2.txt
    |-- lit_review_pivot_idea1.txt
    |-- review_lit_review_idea1.txt
    |-- final_verdict_idea1.txt
    `-- review_final_verdict_idea1.txt
```

## Tips

- The closest papers matter more than the cleverness of your prose. If those papers are poorly chosen, the pipeline will be too generous.
- A premier theory paper needs more than a new parameter or a new application setting. The model must produce genuinely new insight.
- Do not skip Step 6. Citation verification matters because hallucinated theory citations are still hallucinations.
- A pivot is normal. Most promising ideas need at least one serious reframing.
- If the idea keeps failing on the same point, stop patching around it and rethink the core mechanism.

## Requirements

- Access to a strong LLM
- Web search access for Steps 5 and 6
- No coding required - this is a prompt-based pipeline
