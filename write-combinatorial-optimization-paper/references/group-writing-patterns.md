# He-Hao Group Writing Patterns

This synthesis is derived from the seven papers listed in
`paper-corpus.md`. It captures reusable structure and reasoning, not text to
copy verbatim.

## Contents

1. Core research narrative
2. Section-by-section templates
3. Algorithm-description pattern
4. Contribution formulation
5. Experimental argument
6. Journal-specific variation
7. Language and claim control
8. Final review checklist

## Core research narrative

The papers repeatedly use the following argument:

```text
important problem or application
-> precise computational challenge
-> limitation in the best existing methods
-> tailored hybrid or local-search framework
-> one central problem-specific mechanism
-> complementary intensification and diversification
-> benchmark comparison
-> controlled component studies
-> transferable insight
```

The central mechanism usually receives the strongest novelty claim. Supporting
components are framed by their roles:

- crossover or perturbation for exploration;
- local search for intensification;
- repair for feasibility;
- mutation or restart for diversification;
- population updating for quality control;
- candidate restriction, incremental evaluation, or caching for speed.

Avoid presenting all components as equally novel.

## Abstract template

Use six compact moves:

1. Define the problem and its objective.
2. State practical relevance or the main computational difficulty.
3. Introduce the named algorithmic framework.
4. Name the one or two distinctive mechanisms and their roles.
5. Summarize benchmark scope and only verified headline results.
6. Mention component analysis, scalability, generality, or a real case study.

Draft skeleton:

```text
The [problem] aims to [objective] under [key constraints].
It is relevant to [applications] and remains difficult because [bottleneck].
We propose [algorithm name], which combines [global mechanism] with
[local mechanism]. Its distinguishing feature is [mechanism], designed to
[causal role]. Experiments on [benchmarks] show [verified result].
Additional analyses clarify [component/generalization/practical value].
```

Do not include implementation trivia, unsupported percentages, or a full list
of neighborhoods.

## Introduction template

### Paragraph 1: formal problem and objective

Define the graph, pieces, customers, routes, containers, or facilities and the
objective early. State the feasibility conditions in prose before adding a
mathematical model.

### Paragraph 2: relevance and relationships

Give concrete applications and position the problem against one or two better
known relatives. Explain what changes when a constraint or objective is added.

### Paragraph 3: computational status

Summarize what exact methods can solve and why heuristics are required for the
target scale. Use instance sizes and time budgets only when sourced.

### Paragraph 4: method gap

Identify a structural gap, not merely “existing methods are slow.” Examples:

- parent solutions cannot recombine a key configuration;
- direct neighborhoods cannot cross a feasibility barrier;
- the same expensive evaluation is repeated;
- operator selection ignores search feedback;
- existing work treats two related variants separately.

### Paragraph 5: proposed approach

Name the framework, central mechanism, and complementary components. Explain
their causal roles in one paragraph.

### Contributions

Use two to four bullets. A strong ordering is:

1. new problem/model or new central mechanism;
2. complete algorithm and supporting mechanisms;
3. verified computational or practical contribution;
4. code/data/generalization, when applicable.

Each bullet should answer “what,” “why,” and “evidence or scope.”

### Road map

End with one short paragraph describing the remaining sections.

## Literature-review template

Organize the review by the decision or algorithmic gap that motivates the
method, not by a long chronological list.

Useful taxonomies from the corpus include:

- exact versus heuristic;
- hierarchical versus integrated;
- population-based versus neighborhood-based;
- single-depot versus multidepot;
- limited versus unlimited resources;
- problem-specific versus unified frameworks.

Use a comparison table when methods differ across at least three meaningful
dimensions. End the review with a synthesis paragraph:

```text
what the literature solves well
-> what remains difficult
-> why the proposed mechanism is a plausible response
```

## Algorithm-description pattern

### Open with the whole algorithm

Introduce the framework before its components. Provide Algorithm 1 with:

- input and output;
- initialization;
- main stopping loop;
- selection or current-solution choice;
- generation or perturbation;
- repair;
- local improvement;
- best-solution update;
- population update, acceptance, or restart.

Make section order follow pseudocode call order.

### Explain each component in four layers

1. **Purpose:** the search role and bottleneck.
2. **Mechanism:** exact state transition.
3. **Correctness:** feasibility preservation or repair.
4. **Efficiency:** candidate restriction, auxiliary state, incremental
   evaluation, and complexity.

Use a figure for graph assembly, route splitting, geometric feasibility, or
other state changes that are hard to infer from prose.

### Describe neighborhoods reproducibly

For each move, specify:

- selected elements and their source structures;
- removed and inserted elements or edges;
- admissibility and capacity/geometric checks;
- evaluation formula;
- exploration order and first/best-improvement rule;
- tie-breaking and randomization;
- candidate-list restriction;
- complexity.

Group related moves in a table when definitions repeat.

### Discuss complementarity

Add a short discussion after all components:

```text
why global and local mechanisms need each other
-> how feasibility is maintained
-> how search stagnation is avoided
-> what makes the design problem-specific
```

## Contribution formulation

Use this evidence ladder:

| Claim strength | Required support |
|---|---|
| implemented mechanism | active code and correctness checks |
| lower evaluation cost | operation count or complexity comparison |
| faster runtime | matched wall-clock ablation |
| better solution quality | controlled repeated runs |
| statistically better | paired test with disclosed protocol |
| scalable | multi-size or multi-thread scaling evidence |
| generalizable | application or adaptation beyond one setting |
| state of the art | current literature comparison |

Preferred formulation:

```text
We introduce [mechanism] to address [specific bottleneck].
It [operational behavior], which is expected to [causal effect].
Section [x] evaluates this mechanism through [controlled evidence].
```

Avoid:

- “novel” without a literature boundary;
- “efficient” without a baseline;
- “robust” from one seed;
- “high-performance” from parallel code alone;
- “general” without another problem or a structural argument.

## Experimental argument

The corpus typically separates the main comparison from explanatory studies.

### Main evaluation

Report:

- benchmark provenance and instance scale;
- reference methods and availability of code;
- compiler, optimization flags, hardware, OS, and thread count;
- parameter calibration, often with an automatic configurator;
- stopping condition and fairness rationale;
- independent runs and distinct seeds;
- best, average, and time;
- wins/ties/losses and a paired Wilcoxon signed-rank test when appropriate;
- improved or matched bounds only after exact verification.

### Additional experiments

Design variants to answer named questions:

- Does the central crossover or neighborhood help?
- Does the acceleration mechanism reduce time or evaluations?
- Does diversification prevent stagnation?
- Does learning outperform random or static operator selection?
- Does performance persist on larger instances or longer runs?
- Which component matters by instance size?

Disable one mechanism per variant and preserve all other conditions.

### Result narration

Use three layers:

1. report the quantitative observation;
2. state statistical significance;
3. give a mechanism-based interpretation.

Do not infer causality from the main benchmark table alone. Use ablations for
causal statements.

## Journal-specific variation

### Computers & Operations Research

- Use a compact applied narrative.
- Place problem, algorithm, experiments, and additional component studies in
  clearly separated sections.
- Include a real case study when the problem comes from an application.

### European Journal of Operational Research

- Emphasize methodological unification and complementary search components.
- Give a stronger problem-solving methodology discussion.
- Use additional experiments and performance profiles to explain mechanisms.

### INFORMS Journal on Computing / Transportation Science

- State computational and software contribution clearly.
- Use detailed pseudocode, repair procedures, and reproducibility information.
- Explain why the main operator is structurally meaningful.

### Networks

- Give a concise algorithm section with explicit component subsections.
- Emphasize adaptation of a powerful mechanism from a related problem and
  demonstrate scalability on larger instances.

## Language and claim control

Prefer:

- “The algorithm integrates complementary components...”
- “The mechanism is designed to...”
- “The additional experiments isolate the role of...”
- “The results indicate...”
- “This observation suggests...”

Use “first,” “new,” “significant,” and “state-of-the-art” only after checking
their evidence.

Keep equations near the first use of their quantities. Define every acronym
once. Use the same term for a component across pseudocode, prose, figures, and
experiments.

## Final review checklist

- Does the abstract follow the evidence actually available?
- Does the introduction end in a precise research gap?
- Is one mechanism visibly central?
- Does Algorithm 1 match the implementation order?
- Can every move and repair step be reproduced?
- Are speed claims separated from quality claims?
- Does each contribution have a corresponding experiment or a future-tense
  validation plan?
- Are benchmark comparison rules identical to solver objective ordering?
- Are limitations acknowledged without weakening verified findings?
- Does the conclusion summarize findings instead of introducing new claims?
