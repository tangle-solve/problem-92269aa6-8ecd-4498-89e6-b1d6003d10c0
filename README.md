<!-- solve-problem:92269aa6-8ecd-4498-89e6-b1d6003d10c0 -->
# Deterministic polynomial-time Exact Matching

A [Tangle Solve problem](https://solve.tangle.tools/problems/92269aa6-8ecd-4498-89e6-b1d6003d10c0).

## What is the problem?

**Exact Matching (EM):** Given an undirected graph \(G = (V, E)\) where each edge is colored either red or blue, and an integer \(q\), decide whether \(G\) contains a **perfect matching containing exactly \(q\) red edges**. The question: is there a **deterministic polynomial-time** algorithm for this problem?

Formal setting: input \((G, R, B, q)\) with \(R \cup B = E\), \(R \cap B = \emptyset\), \(|V|\) even. Output YES iff \(\exists\) perfect matching \(M \subseteq E\) with \(|M \cap R| = q\). Equivalently: is the coefficient of \(x^q\) in the "matching enumerator" \(R_G(x) = \sum_{M \text{ perfect}} x^{|M \cap R|}\) nonzero?

Note the problem is a *decision* problem about exact counts, not an optimization problem (minimizing/maximizing red edges is solvable by weighting). The natural search version (find the matching) reduces to the decision version via self-reduction.

## Why does it matters

EM is the canonical example of a natural problem solvable by the isolation-lemma–based randomization of Mulmuley–Vazirani–Vazirani (which gave the first randomized NC algorithm for perfect matching) but resisting derandomization for ~40 years. Solving it would likely yield deterministic parallel (RNC → NC) algorithms for matching and advance pseudorandomness for the isolation lemma. It sits inside weighted matching, so a solution has practical appeal for exact-budget assignment problems (scheduling, pairing with quotas).

## What's already known?

- **Randomized poly-time:** Mulmuley, Vazirani & Vazirani (1987) solve EM in RNC (hence randomized poly-time) via the isolation lemma applied to the Tutte matrix with weights \(w(e) = x^{c(e)}\) over a field; the coefficient test on \(\det\) detects exact counts.
- **Special cases solved deterministically:** planar and \(K_{3,3}\)-minor-free graphs (Yuster, 2012); small \(q\) or \(q\) near the maximum red count (Karfinkel, derandomized isolation for bounded counts); bounded genus / bounded treewidth graphs (verify); graphs with few red edges via color-coding.
- **Approaches tried:** direct rank/derandomization of the isolation lemma (fails in general — isolation of a single perfect matching deterministically is itself a major open problem, and full isolation may be *harder* than EM); combinatorial exchange arguments on the lattice of matchings (the "matroid parity"-flavored structure is not a matroid); counting-based approaches hit #P-hardness of computing \(R_G(x)\) exactly.

Key structural fact: matchings of a graph form a basis system of a "matching-greedoid"-like structure; perfect matchings with exactly \(k\) red edges can be counted modulo small primes via reductions to a constant number of rank computations (verify) — used in the planar case.

## What would count as solving it?

**Full solution (upper bound):** A deterministic polynomial-time algorithm deciding EM on arbitrary graphs — equivalently, a deterministic poly-time test for whether the coefficient of \(x^q\) in \(R_G(x)\) is nonzero. A referee would accept a correct algorithm with a proof of poly-time bound.

**Partial but valued results:**
- Derandomization under assumptions (e.g., deterministic isolation for perfect matchings, or hitting sets for the relevant polynomial-identity family of subexponential/quasipolynomial size — even \(n^{O(\log n)}\) would be major progress).
- A deterministic algorithm for any *unconditional* super-constant generalization of known special cases (e.g., \(q = O(\log n)\) improved to \(n^{o(1)}\)... or arbitrary \(q\) on new graph classes).
- **Lower bound direction:** hardness (e.g., EM complete for some class, or reducible to deterministic isolation) would reframe the problem.

## How to start

1. Read Mulmuley–Vazirani–Vazirani (1987) Sections on the isolation lemma and the EM algorithm — understand exactly where randomization enters (choosing random weights isolating a unique perfect matching, then reading off its red count via a single coefficient).
2. Read Yuster (2012) "Fast algorithms for exact matching in planar graphs" (verify exact title) to see the derandomization technique in the planar case — it hints at what structural properties enable determinism.
3. Natural approach: view EM as a polynomial identity testing (PIT) problem for the family \(\{\det(T_G(x))\}\) where \(T_G\) is the colored Tutte matrix; the goal becomes a deterministic hitting set for this structured PIT family. Try to exploit that only one variable \(x\) is involved.
4. Main obstacle: no deterministic analogue of the isolation lemma is known; even quasipolynomial hitting sets for read-once oblivious branching programs were hard-won, and this family is less understood. Avoid trying full derandomization of isolation first — target the *decision* structure of EM directly.

## Key references

- **Papadimitriou, Yannakakis (1982), "The Complexity of Restricted Spanning Tree Problems"** — establishes complexity of constrained subgraph problems in this family (verify precise EM attribution here). Link: not resolvable.
- **Mulmuley, Vazirani, Vazirani (1987), "Matching is as easy as matrix inversion," Combinatorica 7(1)** — proves perfect matching is in RNC via the isolation lemma and gives the randomized poly-time algorithm for Exact Matching. https://doi.org/10.1007/BF02579206
- **Yuster (2012), exact matching in (planar / \(K_{3,3}\)-free) graphs (verify title/venue)** — deterministic algorithms for EM on restricted graph classes.

## Warnings

- EM is a *decision/exact-count* problem; do not conflate with min/max red-edge matching, which is trivially in P via weights.
- Computing \(R_G(x)\) exactly is #P-hard, so exact counting is a dead end; you need nonzeroness of one coefficient.
- The randomized algorithm needs only *isolation* + rank tests; requiring full deterministic isolation is likely stronger than necessary and is itself open.
- Several claimed derandomizations on special cases exist; verify parameters (which \(q\), which graph classes) before building on them.

---
*`ALGO-000122` · unverified*

## Acceptance guidance

**Full solution (upper bound):** A deterministic polynomial-time algorithm deciding EM on arbitrary graphs — equivalently, a deterministic poly-time test for whether the coefficient of \(x^q\) in \(R_G(x)\) is nonzero. A referee would accept a correct algorithm with a proof of poly-time bound.

**Partial but valued results:**
- Derandomization under assumptions (e.g., deterministic isolation for perfect matchings, or hitting sets for the relevant polynomial-identity family of subexponential/quasipolynomial size — even \(n^{O(\log n)}\) would be major progress).
- A deterministic algorithm for any *unconditional* super-constant generalization of known special cases (e.g., \(q = O(\log n)\) improved to \(n^{o(1)}\)... or arbitrary \(q\) on new graph classes).
- **Lower bound direction:** hardness (e.g., EM complete for some class, or reducible to deterministic isolation) would reframe the problem.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/92269aa6-8ecd-4498-89e6-b1d6003d10c0?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000122.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000122)
