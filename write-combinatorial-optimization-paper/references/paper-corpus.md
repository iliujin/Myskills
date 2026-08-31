# Source Paper Corpus

This file summarizes the seven PDFs in
`docs/课题组论文样例学习为skills`. Page references are PDF page numbers.
Use the original PDF when an exact equation, parameter, table entry, or citation
is needed.

## Contents

1. Corpus overview
2. CPTPC with cross-docking
3. Multi-population HGA for CLRP
4. gEAX memetic search for SDVRP
5. Learning-guided ILS for minmax mTSP
6. Memetic search for single/multidepot minmax mTSP
7. HGA for Hamiltonian p-median
8. HGA for TSPs with profits
9. Cross-paper lessons

## Corpus overview

| ID | Problem | Central mechanism | Venue |
|---|---|---|---|
| P1 | Capacitated profitable tour with cross-docking | two-level EAX and streamlined local search | COR 181 (2025) |
| P2 | Capacitated location routing | depot-configuration subpopulations and mdEAX | IJOC (2025) |
| P3 | Split-delivery vehicle routing | general EAX with problem-specific repair/local search | Transportation Science 57(2) (2023) |
| P4 | Minmax multiple TSP | MAB-guided perturbation in iterated local search | COR 185 (2026) |
| P5 | Single/multidepot minmax multiple TSP | unified mEAX memetic search and post-optimization | EJOR 307 (2023) |
| P6 | Hamiltonian p-median | EAX adapted to exactly \(p\) cycles | Networks 83 (2024) |
| P7 | Orienteering and prize-collecting TSP | unified extended EAX for optional vertices | Networks 82 (2023) |

The recurring design principle is to adapt a powerful search mechanism to the
structural difference of the target problem, then support it with local
improvement, feasibility handling, diversification, and controlled experiments.

## P1. Capacitated profitable tour problem with cross-docking

**Citation.** Pengfei He, Wenchong Chen, Qinghua Wu, and Fengjun Xiao,
“Capacitated profitable tour problem with cross-docking,”
*Computers & Operations Research* 181 (2025), 107077.

**Problem.** Select profitable pickup-delivery requests and construct
capacity-feasible pickup and delivery routes through a cross-dock. Maximize
collected request profit minus travel cost. The work originates from an
Industrial Internet logistics application.

**Method.**

- Give an arc-flow model for the new CPTPC.
- Initialize a population with a two-phase randomized greedy construction for
  pickup and corresponding delivery routes.
- Use a two-level edge assembly crossover, EAX2, to assemble pickup- and
  delivery-route edge structures separately; the resulting intermediate
  solution can still violate request consistency or vehicle capacity.
- Restore request consistency and capacity feasibility after crossover.
- Combine nine standard CVRP moves with dedicated add-request and
  served/unserved swap-request moves, under an alpha-nearest restriction.
- Accelerate best-position maintenance for the two request-specific moves with
  priority queues and incremental updates, called streamlined computation.
- Apply objective-and-distance population updating and restart on stagnation.

**Contribution structure.**

1. introduce an application-motivated problem;
2. formulate it mathematically;
3. develop the tailored HGA with EAX2 and streamlined local search;
4. validate it on artificial, related-problem, and real-world instances.

**Evaluation.** Compare 40 small CPTPC instances with CPLEX/Gurobi, adapt the
HGA to 19 VRPCD references, and test 60 medium, 60 large, and three real CPTPC
instances. Use 20 runs and a 300,000-local-search-iteration stopping condition
for each CPTPC instance, apply Wilcoxon tests, disable streamlined computation
and EAX2 separately on the 120 medium/large instances, study longer stopping
conditions, and conduct a real case study.

**Writing lesson.** When a paper introduces a new applied problem, connect the
application, model, dedicated algorithm, benchmark generation, exact validation,
and case study in one evidence chain.

**Page guide.** Abstract/contributions: pp. 1-3; model and Algorithm 1: p. 4;
EAX2 and local search: pp. 5-8; experiments: pp. 8-12; conclusion: p. 12.

## P2. A hybrid genetic algorithm with multi-population for CLRP

**Citation.** Pengfei He, Jin-Kao Hao, and Qinghua Wu,
“A Hybrid Genetic Algorithm with Multi-Population for Capacitated
Location Routing,” *INFORMS Journal on Computing*, Articles in Advance (2025),
DOI 10.1287/ijoc.2023.0416.

**Problem.** Jointly choose capacitated depots and capacity-feasible vehicle
routes to minimize depot opening, vehicle use, and route costs.

**Method.**

- Use a mixed initial depot-configuration strategy. Progressive filtering
  produces candidate configurations and retains at most 100 after
  Clarke-Wright regret evaluation. A coverage-ratio heuristic first balances
  MST-based estimated cost with coverage overlap/geographic dispersion, then
  evaluates a configuration by the mean cost of ten locally improved solutions.
- Organize solutions into subpopulations, each tied to a promising depot
  configuration, plus an extra subpopulation for other configurations.
- Construct that extra subpopulation by adding depots from a rough-cost list
  until selected capacity covers total demand, without the geographic-overlap
  term.
- Select subpopulations and then parents through binary tournaments.
- Apply multi-depot EAX to parents with different depot configurations. Add
  dummy loops to equalize degrees, assemble edges, split mega-tours, and remove
  subtours.
- Restore feasibility in two stages: add a depot if total open capacity is
  insufficient, then apply penalized Relocate, Swap, and two 2-opt-star moves
  with tabu memory and dynamically increased penalties for route/depot
  violations.
- Apply similarity-based ruin/reinsert mutation and ten VND neighborhoods.
- When a new global best uses a previously untracked configuration, replace the
  tracked subpopulation with the worst mean objective and rebuild it. At half
  of the time budget, retain only the better half of the subpopulations; rebuild
  the full population after prolonged stagnation.

**Central insight.** The population hierarchy mirrors the problem hierarchy:
depot configuration at the upper level and routes at the lower level. The
crossover changes both levels rather than treating the location decision as
fixed.

**Evaluation.** Test four sets totaling 281 instances, report 103 improved
upper bounds and 85 matched best-known results, tune with irace, use
single-thread C++, 20 independent runs, a default budget of 300,000 fully
locally searched offspring, and Wilcoxon tests. On the 202 Set-S instances,
compare mixed initialization with each constituent alone, compare 15
subpopulations against 0/5/10, and compare mdEAX with depot-change crossover
variants. Code and data are made available through the IJOC repository.

**Writing lesson.** For a two-level decision problem, align representation,
population organization, crossover, and ablation questions with the same
hierarchy.

**Page guide.** Contributions: pp. 1-2; literature taxonomy: pp. 2-4;
framework: pp. 4-5; initialization: pp. 5-6; mdEAX: pp. 6-7;
repair/mutation/local search: pp. 7-8; population/discussion: pp. 8-9;
main experiments: pp. 9-12; component analysis: pp. 12-14; conclusion: p. 14.

## P3. General edge assembly crossover-driven memetic search for SDVRP

**Citation.** Pengfei He and Jin-Kao Hao,
“General Edge Assembly Crossover-Driven Memetic Search for Split Delivery
Vehicle Routing,” *Transportation Science* 57(2) (2023), 482-511.

**Problem.** Minimize total distance in split-delivery VRP with either limited
or unlimited fleet size, where customer demand may be served by several routes.

**Method.**

- Initialize exactly
  \(K_{\min}=\lceil\sum_i d_i/Q\rceil\) routes, extend them through randomized
  nearest-neighbor insertion without splitting, then greedily split-insert any
  remaining demand; improve each initial individual locally.
- Generalize EAX to graphs whose customer degrees can differ because of split
  deliveries; preserve shared edges and assemble nonshared edges.
- Repair customer-demand balance and vehicle capacity.
- Use diversification-oriented mutation.
- Explore 13 VND neighborhoods: nine classical VRP moves and four
  SDVRP-specific interroute moves, with nearest-neighbor restriction and first
  improvement.
- For the limited-fleet regime, temporarily relax route count during
  mutation/local search and then use route elimination to restore exactly
  \(K_{\min}\) routes; fleet size is not itself optimized.
- Bound excessive splits for selected SDVRP moves with
  \(s_i=\max(s_{\min},\lceil\theta d_i/Q\rceil)\).
- Maintain a clone-free quality-and-distance population and restart after
  prolonged offspring stagnation.

**Central insight.** Edge assembly is generalized beyond equal-degree TSP
graphs. Repair and split-specific neighborhoods make the inherited structure
usable in SDVRP.

**Evaluation.** Test four sets containing 162 base instances under both fleet
regimes, giving 324 instance-regime cases. For limited fleet, report 70 improved
bounds and 75 matches; for unlimited fleet, report 73 improved bounds and 81
matches. Use single-thread C++, 20 seeds, irace, a default 40,000-offspring
budget, and Wilcoxon comparisons. Component studies on 74 unlimited-fleet
instances compare gEAX with giant-tour/no crossover, analyze shared edges in
high-quality solutions, disable neighborhoods and mutation individually, and
vary the maximum-splits rule. The method ranked second in the SDVRP track of
the 12th DIMACS implementation challenge.

**Writing lesson.** Explain why the inherited mechanism fails directly, show
the structural generalization, then show how repair and local search complete
the adaptation.

**Page guide.** Abstract/contributions: PDF pp. 2-3; framework/initialization:
p. 5; gEAX: pp. 5-8; feasibility repair: pp. 8-9; mutation/local search/route
and split controls: pp. 9-10; population: pp. 10-11; main experiments:
pp. 11-14; component analysis: pp. 14-17; conclusion: pp. 17-18.

## P4. Learning-guided iterated local search for minmax mTSP

**Citation.** Pengfei He, Jin-Kao Hao, and Jinhui Xia,
“Learning-guided iterated local search for the minmax multiple traveling
salesman problem,” *Computers & Operations Research* 185 (2026), 107255.

**Problem.** Partition cities among \(m\) depot-returning tours while minimizing
the longest tour.

**Method.**

- Build a greedy randomized initial solution.
- Explore ten route neighborhoods with best improvement, an alpha-nearest
  candidate restriction, and do-not-look filtering.
- When a new local optimum improves the global best, apply EAX-TSP separately
  to every tour and then return to intertour local search.
- Accept local optima through a probabilistic rule.
- Escape local optima through removal and insertion perturbations.
- Use an epsilon-greedy multi-armed bandit to select one of five removal
  operators and one of three insertion operators. Update operator weights every
  100 iterations from rewards for improving the global best, improving the
  current local optimum, or obtaining a probabilistically accepted solution.
- Generate a new initial solution after each fixed 40,000-iteration cycle.

**Central insight.** Learning is applied only where a meaningful online choice
exists: selecting perturbations that leave deep local-optimum basins. It does
not replace the deterministic local improvement mechanism.

**Evaluation.** Test 41 small and 36 large standard instances, report 32
improved upper bounds and 35 matches, use single-thread C++, 20 runs, irace, a
default \((n/100)\times4\)-minute limit, matched stopping conditions, and
Wilcoxon tests. Compare best improvement with first improvement, MAB with
roulette/random selection, standard with long runs, and convergence against
leading methods.

**Writing lesson.** Introduce learning through a concrete search decision and
compare it against simple operator-selection policies, not only against the
full state of the art.

**Page guide.** Contributions and gap: pp. 1-2; Algorithm 1 and local search:
pp. 2-4; perturbation/MAB: pp. 4-5; main experiments: pp. 5-7;
additional studies: pp. 7-9; conclusion: pp. 9-10.

## P5. Memetic search for minmax mTSP with single and multiple depots

**Citation.** Pengfei He and Jin-Kao Hao,
“Memetic search for the minmax multiple traveling salesman problem with single
and multiple depots,” *European Journal of Operational Research* 307 (2023),
1055-1070.

**Problem.** Minimize the longest tour in single-depot and multidepot mTSP
under one unified solver.

**Method.**

- Generate randomized feasible populations and improve every initial solution.
- Adapt EAX to create mEAX for both variants. Eliminate isolated subtours in
  every intermediate solution; for the multidepot variant, additionally split
  any giant tour containing several depots through repeated 2-opt-star moves.
- Retain only the best \(\gamma\) feasible intermediate children for expensive
  VND evaluation.
- Improve offspring using auxiliary evaluation data and six neighborhoods for
  the single-depot variant; disable M3 in the multidepot variant because it can
  return a salesman to the wrong depot.
- Trigger post-optimization only when an offspring improves the global best:
  apply an ejection chain with at most two relocations, use EAX-TSP on the
  changed tours, and repeat while either stage improves the solution.
- Reject clones and select survivors by quality and diversity. On prolonged
  stagnation, contract the population and replace half of it randomly.

**Central insight.** A common memetic skeleton handles both variants; the
crossover's feasibility transformation changes with depot structure. Expensive
single-tour optimization is triggered selectively.

**Evaluation.** Test 77 single-depot and 43 multidepot instances and calibrate
with irace. For single-depot instances, use 20 runs and a
\((n/100)\times4\)-minute limit; for multidepot instances, use a
30,000-iteration limit. Report 44 new bounds and 26 matches for the
single-depot set, and 39 new bounds and one match for the multidepot set.
Apply Wilcoxon tests and performance profiles. On the 77 single-depot
instances, disable mEAX, post-optimization, M3, and M6 separately and analyze
long-run convergence on four representatives.

**Writing lesson.** A unified method is a contribution only when the paper
states what remains common, what changes between variants, and why the shared
mechanisms remain valid.

**Page guide.** Contributions: pp. 1-2; methodology, Algorithm 1, and
initialization: p. 3; mEAX: pp. 3-5; VND: pp. 5-6;
post-optimization/population management: pp. 6-7; main experiments: pp. 7-9;
component studies: pp. 9-12; conclusion: p. 12.

## P6. A hybrid genetic algorithm for Hamiltonian p-median

**Citation.** Pengfei He, Jin-Kao Hao, and Qinghua Wu,
“A hybrid genetic algorithm for the Hamiltonian p-median problem,”
*Networks* 83 (2024), 348-367.

**Problem.** Partition all vertices into exactly \(p\) disjoint Hamiltonian
cycles and minimize their total cost.

**Method.**

- Present the first population-based hybrid search study for this problem.
- Randomly choose \(p\) seeds, greedily extend every cycle to at least three
  vertices, insert remaining vertices by a nearest-neighbor rule, and locally
  improve \(4\mu\) candidates before selecting \(\mu\) by quality and distance.
- Adapt EAX and restore the exact number of cycles with alpha-nearest-restricted
  2-opt-star moves: merge cycles if the intermediate count exceeds \(p\), and
  split cycles if it is below \(p\).
- Explore seven neighborhoods through VND with alpha-nearest restriction.
- With a fixed probability, apply a sequence of cross-cycle M1 or M4
  perturbations to inject edges absent from the parents.
- Update the population with quality-and-distance ranking and restart on
  stagnation.

**Central insight.** The TSP crossover becomes applicable only after adding a
problem-specific transformation that enforces exactly \(p\) cycles.

**Evaluation.** Compare on 145 established instances and introduce 70 larger
instances up to 1060 vertices; report eight improved established bounds,
perform 20 runs, Wilcoxon tests and performance profiles. Compare
\(\beta\in\{3,5,10,15\}\), a no-crossover variant, and a no-mutation variant;
on four representatives, analyze 600 local optima within 5% of the best-known
value to explain why high-quality solutions share edges; examine long-run
scalability.

**Writing lesson.** When transferring a mechanism from a related canonical
problem, state the invariant it violates, the repair that restores the target
problem, and the scale at which the transfer becomes useful.

**Page guide.** Problem and positioning: pp. 1-2; method: pp. 2-7;
main evaluation: pp. 8-10; additional studies: pp. 10-13;
conclusion: p. 14.

## P7. Hybrid genetic algorithm for undirected TSPs with profits

**Citation.** Pengfei He, Jin-Kao Hao, and Qinghua Wu,
“Hybrid genetic algorithm for undirected traveling salesman problems with
profits,” *Networks* 82 (2023), 189-221.

**Problem.** Solve both the orienteering problem, which maximizes collected
profit under a travel budget, and the prize-collecting TSP, which minimizes
travel cost subject to a profit threshold.

**Method.**

- Use one HGA framework for the two primal-dual-style profit variants.
- Generate \(4\lambda\) initial candidates through variant-specific greedy
  construction and local search, then retain \(\lambda\) by survivor selection.
  For OP, construction may temporarily use up to \(1.5\) times the travel
  budget before local search restores feasibility.
- Extend EAX to parent routes with different visited-vertex sets and therefore
  different vertex degrees.
- Improve OP offspring by 2-opt, removal for budget repair, and repeated
  add-plus-2-opt; improve PCTSP offspring by 2-opt, addition for profit repair,
  and repeated remove-plus-2-opt. Restrict addition candidates by
  delta-nearest lists.
- Mutate by removing low-loss visited vertices, forbidding their immediate
  reinsertion, and greedily adding new vertices that E2AX cannot introduce.
- Apply objective-and-distance population management.

**Central insight.** Optional vertices break the equal-degree assumption of
classical EAX. Dummy structures and variant-specific improvement restore a
meaningful edge-assembly process while retaining a shared framework.

**Evaluation.** Use 344 OP instances and 240 PCTSP instances including large
cases, irace-tuned parameters, 20 seeded runs, single-thread C++ execution, and
Wilcoxon comparisons. Report 67 new OP lower bounds with 172 matches; for
PCTSP, report 120 new upper bounds, 96 matches, and 24 cases not reaching the
best-known result. Compare E2AX with giant-tour crossover on OP Sets II/III and
three PCTSP sets. Restrict the no-crossover and no-mutation variants, diversity
analysis, and convergence traces to OP Sets II/III.

**Writing lesson.** For related problems with different objective directions,
separate the common search architecture from variant-specific feasibility and
acceptance rules.

**Page guide.** Problem and method gap: pp. 1-4; Algorithm 1 and HGA:
pp. 4-9; main comparisons: pp. 9-14; component analysis: pp. 14-16;
conclusion: p. 16.

## Cross-paper lessons

### Algorithm design

1. Start from a strong framework but make one structural adaptation central.
2. Preserve meaningful parent building blocks, then repair target-problem
   invariants.
3. Couple expensive global moves with efficient local intensification.
4. Restrict neighborhoods with nearest-neighbor lists or incremental state.
5. Trigger expensive post-optimization only for promising solutions.
6. Explain diversification as a distinct role from local improvement.

### Scientific argument

1. Tie every mechanism to a named bottleneck.
2. State exactly why a canonical operator cannot be used unchanged.
3. Use an ablation for each central causal claim.
4. Report statistical evidence, not only best values.
5. Examine behavior by instance scale; component value often changes with size.
6. Make code, instances, or improved bounds available when possible.

### Writing structure

```text
problem and applications
-> formal definition
-> focused literature taxonomy
-> gap and contributions
-> Algorithm 1
-> components in execution order
-> benchmark protocol
-> main comparison
-> component studies
-> concise conclusion and future work
```
