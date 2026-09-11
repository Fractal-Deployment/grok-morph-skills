# Advanced Analytic Techniques for ArgueForge

This reference provides concise guidance on key structured methods embedded in the ArgueForge protocol. Use these when the main instructions call for them.

**LLMVE factor contests:** also load `llmve-factor-contest.md` (dual-lane, claim_class, three-books, hand-offs).

## Analysis of Competing Hypotheses (ACH)
From intelligence analysis (Richards Heuer / CIA methodology).

**Purpose**: Reduce confirmation bias and improve diagnostic reasoning by systematically evaluating evidence against multiple hypotheses.

**How to apply**:
1. List competing hypotheses (4–7) across the top.
2. List relevant evidence down the side (prioritize diagnostic evidence — items that help distinguish between hypotheses).
3. For each evidence item, score consistency with each hypothesis:
   - +2: Strongly consistent / supports
   - +1: Somewhat consistent
   - 0: Neutral or not applicable
   - -1: Somewhat inconsistent
   - -2: Strongly inconsistent / undermines
4. Calculate inconsistency scores per hypothesis (lower = more consistent with evidence).
5. Re-evaluate: Which hypotheses are most/least supported? What new evidence would be most diagnostic?
6. Update beliefs accordingly. Flag evidence that is consistent with multiple hypotheses (low diagnosticity).

**Best practices**:
- Include disconfirming evidence deliberately.
- Revisit the matrix after new information or debate.
- Use code_execution to build and score the matrix (pandas DataFrame) for larger sets.
- LLMVE: treat dual-lane as two hypotheses first; outcome is A_wins | B_wins | synthesis | abandon — never average into green.

## Toulmin Argumentation Model
Stephen Toulmin's model for practical reasoning.

**Components** (require these for major claims):
- **Claim**: The conclusion or assertion.
- **Data / Grounds**: The evidence or facts supporting it.
- **Warrant**: The reasoning rule or principle that connects data to claim (often implicit — make it explicit).
- **Backing**: Support for the warrant (why the warrant is valid).
- **Qualifier**: Strength of the claim (e.g., "probably", "in most cases", "with high confidence").
- **Rebuttal / Reservation**: Conditions or counter-examples where the claim might not hold.

**Usage in ArgueForge**:
- Structure key arguments in this format during Phase 2.
- Critique focuses heavily on the warrant and rebuttal sections.
- Helps surface hidden assumptions and makes arguments more robust and falsifiable.
- LLMVE: Qualifier must include claim_class; Rebuttal must name residual falsify_if.

## Pre-Mortem Analysis
Gary Klein's technique to improve forecasting and reduce overconfidence.

**Purpose**: Counteract optimism bias and groupthink by assuming failure in advance.

**How to run** (for promising hypotheses or recommendations):
1. Assume it is 3–5 years in the future and the hypothesis/strategy has failed badly or produced major negative unintended consequences.
2. Generate a list of plausible reasons why it failed (5–10+). Be creative and specific.
3. For each reason, identify early warning signals that would have been visible.
4. Brainstorm mitigations or adjustments that could have prevented or reduced the failure.
5. Update the original analysis with these insights (risks, indicators, revised recommendations).

**When to use**: Especially on top 2–3 hypotheses in Phase 2 or before final recommendations.

**LLMVE required pre-mortem path**: "Tournament winner was treated as omega_was_measured / training_cleared" — list early signals and mitigations (claim_class discipline, hand-off to compute skill).

## Multi-Criteria Decision Analysis (MCDA) & Consilience Scoring
For tournament selection and synthesis.

**Core idea**: Make trade-offs explicit and weighted rather than intuitive.

**Steps in ArgueForge**:
1. Define 5–8 criteria relevant to the topic (see main SKILL.md for suggested list including Consilience).
2. Weight the criteria (Price’s Law/Pareto Arbiter leads; consider sensitivity analysis on weights).
3. Score each finalist option/hypothesis on each criterion (0–10 or 1–5 scale). Justify scores briefly.
4. Compute weighted scores. Run sensitivity (what if weights change?).
5. Identify robust options (high scores across reasonable weight variations) vs. brittle ones.
6. For synthesis: Look for elements that score highly on high-weighted criteria across multiple options.

**Consilience bonus**: Actively reward hypotheses where multiple independent lines of evidence (different methods, domains, or data sources) converge on the same conclusion. This is a strong signal of reliability.

**LLMVE residual-honesty criterion**: claim_class integrity, three-books, dual-lane, apparatus match, falsify_if specificity. Eloquence without honesty must not win.

## Additional Supporting Techniques
- **Multiple Working Hypotheses** (T.C. Chamberlin): Generate several plausible explanations early and hold them in parallel to avoid premature attachment to one.
- **After-Action Review (AAR)**: After each major phase, ask: What was supposed to happen? What actually happened? Why the difference? What will we do differently next time?
- **Bayesian Updating mindset**: Treat beliefs as probabilities. Explicitly ask "How much does this new evidence move my estimate?" rather than binary true/false.
- **Scenario Planning (2x2 matrices)**: For high-uncertainty topics, identify two key independent uncertainties, create four plausible futures, and test recommendations against them.
- **Dual-lane (LLMVE)**: Two apparatus/readings; falsify; A_wins | B_wins | synthesis | abandon — not dual-proof.

Use these techniques explicitly when the main protocol calls for structured analysis. They raise the epistemic quality of the output significantly.
