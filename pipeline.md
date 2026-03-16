# Theory Research Idea Evaluation Pipeline

Goal: take a theory-oriented research idea and iteratively evaluate, pivot, and defend it until it reaches premier operations management, quantitative marketing, or information systems journal quality.

## Pipeline Overview

```
1. EVALUATE -> 2. REVIEW EVAL -> Score >= 7?
                                 | yes
                                 v
                           5. LIT REVIEW
                                 |
                           6. VERIFY LIT REVIEW
                                 |
                           7. FINAL VERDICT
                                 |
                           8. REVIEW FINAL VERDICT -> Score >= 7? -> DONE
                                 |
                                 no
                                 v
                           3. PIVOT -> 4. EVAL PIVOT
                                 ^          |
                                 |----------|
                                 if score dropped or stayed flat, pivot again
```

If Step 2 finds the critique unfair, re-run Step 1. If Step 8 scores the project below 7, return to Step 3 with the full history. Maximum 3 pivot iterations before recommending a different idea.

## Step 1: Evaluate Idea

Prompt file: `prompt_ideas.txt`

Purpose: critically evaluate whether the idea has the novelty, theoretical insight, tractability, and journal fit required for `Management Science`, `MSOM`, `POM`, `Marketing Science`, or `ISR`.

Input:
- Student's idea in `idea_template.txt` format
- 3 closest papers or models, with URLs

Output:
- `eval_[name]_idea[N].txt`

Evaluation dimensions:
1. Novelty and marginal contribution relative to the closest models
2. Model innovation and mechanism
3. Insight depth and comparative statics
4. Tractability, proof burden, and rigor
5. Relevance and substantive significance
6. Target-journal fit

## Step 2: Review Evaluation

Prompt file: `review_eval_prompt.txt`

Purpose: check whether the Step 1 critique is fair, accurate, and calibrated to theory standards rather than empirical standards.

Input:
- Original idea
- Step 1 evaluation

Output:
- `review_[name]_idea[N].txt`

Loop:
- If the review finds the critique unfair or miscalibrated, re-run Step 1 with corrections.

## Step 3: Pivot Idea

Prompt file: `pivot_prompt.txt`

Purpose: reshape the idea without abandoning the student's core phenomenon. A good pivot usually sharpens the benchmark, changes the primitive that drives the result, simplifies the model, or reframes the contribution around a cleaner managerial insight.

Input:
- Full history: original idea, evaluation, review, and any prior pivots

Output:
- `pivot_idea[N].txt`
- `pivot_idea[N]_v2.txt`, `pivot_idea[N]_v3.txt`, if iterating

The pivot should produce:
- A clear benchmark model
- One non-trivial new ingredient
- Explicit timing, players, and equilibrium concept
- 3-5 propositions or comparative statics
- A tractability and proof plan
- A realistic target journal and framing

## Step 4: Evaluate Pivot

Prompt file: `prompt_ideas.txt`

Purpose: re-score the pivot under the same criteria as Step 1.

Input:
- Pivoted idea
- Original 3 closest papers or models

Output:
- `eval_pivot_idea[N].txt`
- `eval_pivot_idea[N]_v2.txt`, if iterating

Decision:
- If the score drops or stays flat, return to Step 3 with the full history and explain why the last pivot failed.

## Step 5: Literature Review

Prompt file: `lit_review_prompt.txt`

Purpose: run a threat search for novelty. The goal is not a broad literature review; it is to identify the nearest competing models, papers, and working papers that could weaken the contribution.

Input:
- Pivoted idea
- Student's 3 cited papers or models

Output:
- `lit_review_pivot_idea[N].txt`

Web search required:
- Every cited paper must include a verifiable URL.
- Search beyond the student's list for recent working papers and adjacent-field threats.

Threat categories to emphasize:
- Same friction or primitive
- Same timing or information structure
- Same comparative statics or qualitative insight
- Same substantive setting with only minor modeling differences
- Recent working papers that appear to be running the same race

## Step 6: Verify Literature Review

Prompt file: `verify_lit_review_prompt.txt`

Purpose: verify every citation, correct bad metadata, remove fabricated papers, and tighten the threat assessment.

Input:
- Step 5 output file with edit access

Output:
- Edited `lit_review_pivot_idea[N].txt`
- `review_lit_review_idea[N].txt`

Web search required:
- Verify citations through Google Scholar, SSRN, publisher pages, and IDEAS/RePEc when useful.

You must:
- Add URLs for every verified paper
- Remove fabricated or unverifiable citations
- Correct authors, year, journal, and title errors
- Reassess whether each paper is truly a threat

## Step 7: Final Verdict

Prompt file: `final_verdict_prompt.txt`

Purpose: synthesize the full history into a bottom-line verdict on whether the idea should proceed, pivot again, or be abandoned for this target set of journals.

Input:
- Full history

Output:
- `final_verdict_idea[N].txt`

The verdict should include:
1. Final score
2. Top remaining threats
3. Suggested title and abstract
4. Recommended primary and backup journal
5. Key risk
6. Preconditions for proceeding

## Step 8: Review Final Verdict

Prompt file: `review_final_verdict_prompt.txt`

Purpose: make sure the final verdict is fair, internally consistent, and aligned with the evidence gathered earlier in the pipeline.

Input:
- Full history
- Step 7 output

Output:
- `review_final_verdict_idea[N].txt`

Decision:
- If score < 7, return to Step 3 with the full history.

## File Organization

```
IdeaEvaluation/
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
`-- [student_name]/
    |-- [student_name].md
    |-- idea.txt
    |-- eval_[name]_idea1.txt
    |-- review_[name]_idea1.txt
    |-- pivot_idea1.txt
    |-- pivot_idea1_v2.txt
    |-- eval_pivot_idea1.txt
    |-- eval_pivot_idea1_v2.txt
    |-- lit_review_pivot_idea1.txt
    |-- review_lit_review_idea1.txt
    |-- final_verdict_idea1.txt
    `-- review_final_verdict_idea1.txt
```

## Recommended Tooling

| Step | Model capability | Web search |
|------|------------------|------------|
| 1, 2, 3, 4, 7, 8 | Strong theory judgment | No |
| 5 | Strong theory judgment | Yes |
| 6 | Strong theory judgment + careful verification | Yes |

All steps can be parallelized across students or ideas. Steps within a single idea must remain sequential.
