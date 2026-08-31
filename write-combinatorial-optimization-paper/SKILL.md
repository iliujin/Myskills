---
name: write-combinatorial-optimization-paper
description: Extract, evaluate, structure, draft, and review operations-research and combinatorial-optimization papers from solver code, research logs, experiment data, and related PDFs. Use when Codex must align a manuscript with an implemented algorithm, formulate defensible contributions, describe a hybrid genetic or local-search method, design computational studies, or emulate the He-Hao research-group writing pattern for 2DIBPP, routing, location, TSP, and related metaheuristics.
---

# Write a Combinatorial Optimization Paper

Turn implementation evidence into a precise OR paper. Preserve the actual algorithm,
separate engineering choices from scientific mechanisms, and never invent novelty or
experimental evidence.

## Route the references

Read only the references needed for the current task:

- Read [paper-corpus.md](references/paper-corpus.md) when comparing with or learning
  from the seven source papers.
- Read [group-writing-patterns.md](references/group-writing-patterns.md) when drafting
  an abstract, introduction, method, experiment section, or conclusion.
- Read [2dibpp-application.md](references/2dibpp-application.md) for this repository's
  solver, current paper decisions, contribution candidates, and prohibited claims.

For 2DIBPP work, also inspect `AGENTS.md`, `research_log.md`, the active code, and the
latest result files before writing. Treat these as mutable sources of truth.

## Establish the evidence contract

1. Identify the requested deliverable and excluded scope.
2. Rank evidence in this order:
   active code and verified outputs; current research log; manuscript source;
   user-confirmed decisions; intended but unimplemented ideas.
3. Trace the active call path from the executable entry point before treating
   a declared class or function as part of the solver. Exclude dormant,
   commented-out, empty, test-only, or unreachable components.
4. Build an internal alignment table with:
   `claim | code mechanism | mathematical meaning | evidence | status`.
5. Mark a claim as one of:
   `verified`, `implemented-unmeasured`, `planned`, or `unsupported`.
6. For performance claims, record mechanism correctness and measured effect
   separately. A verified implementation can still have an
   `implemented-unmeasured` speed or quality effect.
7. Check result-file provenance: generation date or commit, output schema,
   objective definition, settings, and compatibility with the active code.
   Treat stale or incompatible outputs as unsupported evidence.
8. Remove unsupported claims. Describe planned experiments in future tense only.

Do not equate a class name, container, hash map, thread pool, or cache with a paper
contribution. First identify the algorithmic role and measurable consequence.

## Fix the problem contract

State before drafting:

- sets, decisions, constraints, and feasible-solution definition;
- primary and secondary objectives, including tie-breaking order;
- allowed rotations, resources, capacities, and instance assumptions;
- exact meaning, range, and direction of every reported metric;
- comparison rule used by the solver and by result tables.

Use one objective definition consistently in selection, acceptance, best-solution
updates, tables, and prose. Report all components of a lexicographic objective.

## Derive contributions from mechanisms

For each candidate contribution, complete this chain:

```text
problem-specific bottleneck
-> proposed mechanism
-> why the mechanism changes the search or cost
-> expected measurable effect
-> evidence required
-> possible generality beyond the target problem
```

Prefer two or three supported contributions over a long feature list. Distinguish:

- problem/model contribution;
- search contribution, such as a representation, crossover, or neighborhood;
- acceleration contribution that changes the cost of repeated search operations;
- empirical contribution, such as new bounds or validated scalability.

Do not claim empirical contribution before experiments exist. Do not claim
state-of-the-art or first use without a current literature check.

## Organize the algorithm section

Present the method in execution order:

1. Give one overview paragraph and one high-level pseudocode algorithm.
2. Define the solution representation and its invariants.
3. Explain initial-solution generation.
4. Explain global exploration, parent selection, recombination, repair, and mutation.
5. Explain local intensification and each problem-specific neighborhood.
6. Explain feasibility evaluation and acceleration mechanisms.
7. Explain population or restart management only if active in the implementation.
8. Give time and memory complexity where it clarifies a claimed advantage.
9. State stopping rules and deterministic or stochastic tie-breaking.

For every operator, specify input, output, changed state, feasibility conditions,
acceptance rule, and worst-case or amortized cost. Explain complementary roles:
global exploration, local intensification, diversification, and computational
acceleration.

## Write in the learned group pattern

Use an answer-first, evidence-oriented progression:

```text
application or canonical problem
-> precise formulation
-> computational gap
-> proposed framework
-> distinctive mechanisms
-> benchmark evidence
-> component-level understanding
```

Use cautious claims such as “is designed to,” “reduces repeated evaluation,” or
“the results indicate.” Reserve “demonstrates,” “significantly outperforms,” and
“scales” for direct evidence.

Keep component descriptions causal:

```text
mechanism -> search behavior -> performance consequence
```

Avoid code identifiers in the manuscript unless they denote an algorithm. Translate
implementation into method language, but retain enough detail for reproducibility.

## Design experiments only when requested

When experiments are in scope, separate:

1. benchmark instances;
2. parameter setting;
3. reference algorithms and fairness conditions;
4. hardware, compiler, thread count, run count, seeds, and stopping criterion;
5. main solution-quality comparison;
6. component ablations;
7. runtime, convergence, memory, and scalability;
8. statistical tests;
9. practical case study, only when real data exist.

Use paired variants that disable exactly one mechanism. Keep all other parameters,
seeds, budgets, and hardware fixed. Report best, average, time, wins/ties/losses,
and a paired statistical test when justified. For hierarchical objectives, report
and compare every objective component in the declared order.

If experiments are excluded, stop after defining the future validation matrix. Do
not manufacture tables or numerical improvements.

## Review the finished draft

Check all of the following:

- every contribution appears in the method and has an evidence route;
- every active algorithm component is described, and no inactive component is claimed;
- symbols and objective directions are consistent across sections;
- pseudocode call order matches the implementation;
- each claimed component is reachable through the active production call graph;
- complexity claims name the repeated operation and comparison baseline;
- tables use the same ranking rule as the solver;
- result files use the current objective and output schema;
- ablations isolate one causal mechanism;
- the conclusion contains no stronger claim than the results;
- limitations and future work do not contradict the implemented scope.

Return unresolved discrepancies explicitly instead of silently choosing a version.

## Preferred deliverables

For code-paper alignment, return:

```text
paper claim | code evidence | alignment | required correction
```

For contribution design, return:

```text
contribution | bottleneck | mechanism | rationale | validation | claim strength
```

For drafting, provide clean manuscript prose followed by a short evidence note listing
which facts still require literature or experimental validation.
