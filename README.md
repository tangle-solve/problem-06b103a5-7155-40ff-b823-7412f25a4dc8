<!-- solve-problem:06b103a5-7155-40ff-b823-7412f25a4dc8 -->
# Decidability of 4-sphere recognition

A [Tangle Solve problem](https://solve.tangle.tools/problems/06b103a5-7155-40ff-b823-7412f25a4dc8).

## What is the problem?

**Input:** A finite triangulation (simplicial complex) of a closed topological 4-manifold $M$, given as a list of gluings of 4-simplices.

**Question:** Is $M$ homeomorphic to the 4-sphere $S^4$? Decide this problem algorithmically — i.e., exhibit a Turing machine that halts on every input with the correct yes/no answer — or prove no such algorithm exists.

**Formal setting.** Homeomorphism is meant in the *topological* category (not PL, not smooth). Two interpretations must be distinguished:

1. **Topological recognition:** decide if $M \cong_{\text{Top}} S^4$. This is the canonical open problem.
2. **PL recognition:** decide if $M \cong_{\text{PL}} \partial\Delta^5$ (the boundary of the 5-simplex). A PL certificate of sphericity is checkable (just exhibit a collapsible subdivision), so sphericity is semi-decidable; the hard part is certifying non-sphericity.

Note the input manifold is assumed a manifold; alternatively one may fold in "is this a manifold?" — that subproblem is decidable in all dimensions via local homology checks (verify).

Key structural facts constraining any solution: in dimension 4, PL and smooth categories coincide, and there exist *exotic* smooth/PL 4-spheres (candidate and some confirmed, e.g., Akbulut's and Gabai's constructions of contractible exotic boundary spheres — verify current status) — but Freedman's theorem says every homotopy 4-sphere is homeomorphic to $S^4$.

## Why does it matter?

This is one of the sharpest open decidability questions in topology: it sits exactly at the boundary between dimension 3 (decidable, via Rubinstein–Thompson/normal surfaces and Haken machinery) and dimensions $\geq 5$ (undecidable, via Novikov/Markov). A decidability proof would likely yield an algorithmic 4D theory (e.g., effective versions of Freedman's disk-embedding theorem); an undecidability proof would show the failure of any effective handle/certificate structure in dimension 4, and would be strong evidence that 4-manifold classification is algorithmically hopeless. It also gates the smooth 4-dimensional Poincaré conjecture: an algorithm deciding PL sphericity plus a single exotic sphere counterexample would settle it.

## What's already known?

- **Dimensions $\geq 5$:** Recognizing $S^n$ for $n \geq 5$ (some sources say $n \geq 6$; the boundary cases deserve checking) is undecidable. The proof (Novikov/Markov, via Adian–Rabin) reduces the triviality problem for finitely presented groups to sphere recognition using constructions with two non-simply-connected summands that cancel topologically iff the group is trivial.
- **Dimension 3:** Decidable. Rubinstein (1992) and Thompson gave algorithms via almost-normal surfaces in a triangulation times $S^1$; later simplified by Schleimer and by Burton–Downs–Spreer–S (verify last citation). Implemented in practice (Regina).
- **Dimension 4, partial results:**
  - Sphericity is **semi-decidable**: exhibit a sequence of Pachner moves to the boundary of the 5-simplex; or a collapsible second derived subdivision.
  - If $M$ is given with no 2-torsion in $H_1$, "not a homotopy 4-sphere" is decidable via $\pi_1$ computation (finite presentation computable; triviality of $\pi_1$ is undecidable in general, but abelianization is computable) and homology.
  - The triviality of $\pi_1$ is undecidable in general, so any algorithm must bypass fundamental group computation — this is the central obstruction and the reason high-dimensional undecidability does not directly descend.
  - Freedman (1982): homotopy 4-sphere $\Rightarrow$ homeomorphic to $S^4$ (with Casson–Gordon 2-torsion subtleties, later resolved by Freedman for general case). So the *topological* problem reduces to deciding whether $\pi_1(M) = 1$ *as a topological invariant test*, not as a group-theoretic test — the group may be trivial in ways no algorithm certifies.
  - Hilali; Nabutovsky–Weinberger studied the *geometric* complexity (unsolvability of recognizing standard PL sphere in dim ≥ 5; distance of triangulations); Sokan's thesis and papers on recognition problems for simply connected manifolds (verify).

## What would count as solving it?

Any one of:

1. **Decidability (upper bound):** A Turing machine and correctness proof that halts on all finite triangulations of closed 4-manifolds, answering topological $S^4$-recognition.
2. **Undecidability (lower bound):** A reduction from a known undecidable problem (e.g., group triviality) to $S^4$-recognition in dimension 4 — this requires circumventing Freedman, i.e., a construction where topological sphericity still encodes group-theoretic information, which is precisely what fails in the standard arguments.
3. **Variant results that count as major progress:** decidability of PL 4-sphere recognition; decidability restricted to simply-connected inputs (this is plausibly the right subproblem, since Freedman reduces topological recognition to homotopy recognition); semi-decision procedures for non-sphericity in restricted classes.

A referee would accept: full proof in either direction, or a rigorous algorithm with termination proof (not just heuristics like Regina's practical recognition attempts).

## How to start

1. **First subproblem: simply-connected inputs.** Given $\pi_1(M)=1$ as a promise, decide homotopy equivalence to $S^4$ (check $H_2 = 0$, and the homeomorphism follows by Freedman). Study whether the simply-connectedness *promise* can be replaced by a certificate. Read Freedman–Quinn's book, Chapter 1–2, for the exact statement and its effective content.
2. **Try to port the 3D normal/almost-normal surface machinery.** Read Schleimer's "Sphere recognition lies in NP" and Burton et al. on the 3D algorithm; the obstruction is that normal surface theory in 4-manifolds gives infinite normal 2-spheres lacking the matching theory of normal disks; also $M \times S^1$ tricks degenerate.
3. **For an undecidability attempt:** understand exactly why the Novikov/Markov construction needs dimension ≥ 5 (spun manifolds, thickening of group presentations to 4-complexes — the thickening lands *in* dimension 4, but the recognition problem is shifted up). Read the survey treatment in Poonen's "Undecidable Problems: A Sampler," §4–5, and Nabutovsky–Weinberger on algorithmic aspects of homeomorphism problems.
4. **Main obstacle to keep in mind:** Freedman collapses all topological 4-sphere information to $\pi_1$, but $\pi_1$ triviality is group-theoretically undecidable — yet no known construction forces the *only* witness of nontriviality into a form a recognizer must detect. Any algorithm likely needs an effective/constructive version of disk embedding (currently none exists — a known open subproblem, cf. "is the disk embedding theorem constructive?" discussions).

## Key references

- B. Poonen, *Undecidable Problems: A Sampler*, arXiv:1204.0299. — A modern survey presenting inter alia the undecidability of manifold homeomorphism problems in high dimensions, with clean statements of the Novikov/Markov framework.
- M. Freedman and F. Quinn, *Topology of 4-Manifolds*, Princeton Univ. Press, 1990. — Proves the disk embedding theorem and the homotopy-4-sphere theorem (the topological classification tool any algorithm must effectively harness).
- S. Matveev, *Algorithmic Topology and Classification of 3-Manifolds* (2nd ed.), Springer. — Contains the decidability of 3-sphere recognition and surrounding normal-surface theory; the natural baseline for dimension-lifting attempts.
- S. Schleimer, "Sphere recognition lies in NP," arXiv:math/0703043. — Places 3-sphere recognition in NP via normal surfaces; the cleanest account of why dimension 3 is decidable.
- A. Nabutovsky and S. Weinberger, various papers on algorithmic unsolvability in geometry/topology (e.g., "Algorithmic aspects of homeomorphism problems," 1996) (verify exact title/venue). — Establish that in high dimensions even the *quantitative* complexity of recognizing standard spheres is wild; motivates why dimension 4 is the lone candidate for decidability.
- A. A. Markov, "Insolubility of the problem of homeomorphy" (1958, in Russian) (verify); original undecidability of manifold homeomorphism in dimension ≥ 4 — note: Markov's original statement concerns homeomorphism of manifolds of dimension ≥ 4 (verify whether ≥ 4 or ≥ 5 applies to sphere recognition specifically).

## Warnings

- **PL vs. topological vs. smooth:** In dimension 4, PL = smooth, but Top differs (exotic spheres possible). State clearly which category you target; the census phrasing "homeomorphic to $S^4$" means topological. An exotic smooth structure is still a YES instance topologically.
- **Dimension boundary confusion:** Some sources state undecidability for sphere recognition starting at dimension 5, others at 6; Markov's homeomorphism-undecidability is for dimension ≥ 4 but may not directly give sphere recognition at dimension 4 (verify before citing). The standard belief is: 4D sphere recognition is the open case; verify any claimed ≥ 4 undecidability result carefully.
- **Group-theoretic trap:** "Compute $\pi_1$ and check triviality" is not an algorithm — triviality of finitely presented groups is undecidable (Adian–Rabin). Many naive proposals die here.
- **Freedman is non-effective:** The disk embedding theorem involves infinite processes (Casson handles); no constructive version is known, and this is widely believed to be the core difficulty.
- **Semi-decidability asymmetry:** Yes-instances are semi-decidable (PL certificate); a full decision procedure is equivalent to semi-deciding non-sphericity, since combining semi-decision procedures decides. Focus attacks there.
- The census's field labels ("computational number theory, lattices") are inaccurate — this is computational topology.

---
*`ALGO-000208` · unverified*

## Acceptance guidance

Any one of:

1. **Decidability (upper bound):** A Turing machine and correctness proof that halts on all finite triangulations of closed 4-manifolds, answering topological $S^4$-recognition.
2. **Undecidability (lower bound):** A reduction from a known undecidable problem (e.g., group triviality) to $S^4$-recognition in dimension 4 — this requires circumventing Freedman, i.e., a construction where topological sphericity still encodes group-theoretic information, which is precisely what fails in the standard arguments.
3. **Variant results that count as major progress:** decidability of PL 4-sphere recognition; decidability restricted to simply-connected inputs (this is plausibly the right subproblem, since Freedman reduces topological recognition to homotopy recognition); semi-decision procedures for non-sphericity in restricted classes.

A referee would accept: full proof in either direction, or a rigorous algorithm with termination proof (not just heuristics like Regina's practical recognition attempts).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/06b103a5-7155-40ff-b823-7412f25a4dc8?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000208.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000208)
