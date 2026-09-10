---
tags: [academics, graph-theory, nptel, guide]
type: guide
---

# Watch Guide, what to watch and what is not covered

Index: [[NPTEL Index]] · Resources: [[Course Resources]] · Hub: [[Graph Theory]]

> Playlist: [Graph Theory — Dr. L. Sunil Chandran, IISc (40 lectures)](https://www.youtube.com/playlist?list=PL612CE2AB6F38DF9A)
> Course page: [NPTEL 106108054](https://nptel.ac.in/courses/106108054)
> Lecture 1 direct link: [Introduction: Vertex Cover and Independent Set](https://www.youtube.com/watch?v=Gc8emFk-2vc)

Open the playlist and click the lecture number given in each table below, the playlist is in order, so lecture N is the Nth video. Each runs about 56 minutes.

---

## Read this before you start

The NPTEL course does not begin where my class began. Chandran's Lecture 1 opens at vertex cover and independent set, he *assumes* all the preliminaries, Euler circuits, trees and bipartite basics as prior knowledge. So the first three weeks of my class have no matching videos; those came from Diestel and West.

That means the videos and my class are not aligned lecture-for-lecture. Use the tables below rather than watching in order.

---

## Only the topics my class has actually taught (as of 19 Aug)

Just five lectures, 01 to 05. About 4¾ hours. Nothing else in the 40 is relevant yet.

| | Lecture, click to watch | Which class it matches | My notes |
|---|---|---|---|
| 01 | [Vertex Cover and Independent Set](https://www.youtube.com/watch?v=Gc8emFk-2vc) | 29 Jul, vertex covers, α′ ≤ β ≤ 2α′, MIS | [[2026-07-29 Matchings 2 — Berge and König]] · [[Lec 01 — Vertex Cover and Independent Set]] |
| 02 | [König's and Hall's Theorems](https://www.youtube.com/watch?v=IRbggk6J0TA) | 29 Jul (König) + 10 Aug (Hall) | [[2026-07-29 Matchings 2 — Berge and König]] · [[2026-08-10 König by Induction, Hall, and Factors]] |
| 03 | [More on Hall's Theorem](https://www.youtube.com/watch?v=BGCqWa33OD8) | 10 Aug, k-regular bipartite, factors, defect Hall | [[2026-08-10 König by Induction, Hall, and Factors]] · [[Lec 03 — More on Hall's Theorem and Applications]] |
| 04 | [Tutte's Theorem](https://www.youtube.com/watch?v=PM1FncPlXnM) | 19 Aug. Tutte's 1-factor theorem | [[2026-08-19 Tutte's 1-Factor Theorem]] |
| 05 | [More on Tutte's Theorem](https://www.youtube.com/watch?v=_SOZz_aqRP4) | 19 Aug, likely where Petersen's theorem lives | [[2026-08-19 Tutte's 1-Factor Theorem]] §7 |

Stop at 05. Lecture 06 (*More on Matchings*, covering Tutte–Berge, Edmonds' blossom algorithm) is the next thing coming but has not been taught yet.

### Partial matches, don't be thrown

- Lecture 03 also covers SDRs, Latin squares and Birkhoff–von Neumann, which my class did *not* do. Extra, not examinable from class.
- Lecture 01 covers edge covers and ρ in more depth than my class did.

---

## Roughly half my class has no video at all

This is the part worth internalising: of the nine notes so far, four and a half have no NPTEL coverage whatsoever, because Chandran assumes them as prior knowledge.

| Taught in class | Sessions | Video? |
|---|---|---|
| Preliminaries, edge density, δ≥k lemmas, long-path theorem | 24 Jul (×2) | none |
| Euler circuits. Euler's theorem, both proofs, Königsberg | 27 & 29 Jul | none |
| Trees, MIS in trees (greedy + DP) | 29 Jul | none |
| Tutorial 1, hypercubes, girth bounds, induced paths, Helly | 31 Jul | none |
| Matchings, Berge, König, Hall, Tutte, Petersen | 29 Jul – 19 Aug | Lec 01–05 |

For the no-video half, my own notes plus Diestel Ch. 1 are the only revision sources. [[Master Notes]] Levels 0–6 cover exactly that ground.

---

## The rest, in my syllabus order

| Syllabus topic | Lectures | Notes written? |
|---|---|---|
| Matchings in general graphs. Tutte | 04, 05, 06 | ☐ |
| 2-connected graphs, ear decomposition | 09 | ☐ |
| Menger's theorem | 10 | ☐ |
| Dirac's extensions (k-linkedness) | 11 | ☐ |
| Edge connectivity | 09, 10, 11, 12 | ☐ |
| Vertex colouring, greedy, degeneracy, Brooks | 13, 14 | ☐ |
| Edge colouring. König, Vizing | 15, 16 | ☐ |
| Colouring of planar graphs | 17 | ☐ |
| Perfect graphs | 23, 24, 25, 26, 27 | ☐ |
| Hamiltonian graphs | 28, 29, 30 | ☐ |
| Network flows, structure of minimum cuts | 31, 32, 33, 34 | ☐ |
| Ramsey-theoretic problems | 36 | ☐ |

---

## What the videos do not cover

Three different kinds of gap. They need different fixes.

## Gap 1. On my syllabus, but in no NPTEL lecture

| Topic | Where to get it instead |
|---|---|
| Discharging method | West, planar graphs chapter. Nothing in the 40 lectures touches it. |

This is the one genuine hole. It's an examinable syllabus topic with zero video coverage, so it has to come from the book.

## Gap 2. Taught in my class, but not in NPTEL

Chandran assumes these as background, so there's no video to revise from.

| Taught | My class notes | Where to revise |
|---|---|---|
| Euler circuits, two full sessions (27 & 29 July) | [[2026-07-27 Euler Circuits]] · [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] | West / Diestel Ch. 1 |
|  | Preliminaries: degree, density, extremal arguments | [[2026-07-24 Preliminaries]] · [[2026-07-24 Long Path Theorem]] |
| Diestel Ch. 1 |  | Trees, bipartite characterisation |
| [[2026-07-24 Preliminaries]] §8–9 | Diestel Ch. 1 |  |
| Hypercubes, Helly property, tutorial problems | [[Tutorial 1]] | Diestel Ch. 1 exercises |

> Worth noticing: Euler circuits got two sessions in class but appear nowhere in the video course, and they aren't on the written syllabus either. My notes are the only record.

## Gap 3. In NPTEL, but not on my syllabus, safe to skip

12 of the 40 lectures. Skipping them saves roughly 11 hours.

|  | Title | Why skip |
|---|---|---|
| 07 | Dominating Set, Path Cover | not on syllabus |
| 08 | Gallai–Milgram, Dilworth's Theorem | not on syllabus *(though Dilworth is part of the min-max family, see Bridge 7.1 in [[Master Notes]])* |
| 18 | Proof of Kuratowski's Theorem, List Colouring | syllabus wants planar colouring, not Kuratowski's proof |
| 19 | List Chromatic Index | not on syllabus |
| 20 | Adjacency Polynomial, Combinatorial Nullstellensatz | not on syllabus |
| 21 | Chromatic Polynomial, k-Critical Graphs | not on syllabus |
| 22 | Gallai–Roy, Acyclic Colouring, Hadwiger | not on syllabus |
| 12 | Minors, Topological Minors, k-Linkedness | partially relevant to connectivity, skim rather than skip |
| 35 | Random Graphs, Probabilistic Method: Preliminaries | syllabus wants Ramsey only (Lec 36) |
| 37 | High Girth and High Chromatic Number | not on syllabus |
| 38 | Second Moment Method, Lovász Local Lemma | not on syllabus |
| 39 | Graph Minors and Hadwiger's Conjecture | not on syllabus |
| 40 | More on Graph Minors, Tree Decompositions | not on syllabus |

---

## Time budget

|  | Lectures | Hours (≈56 min each) |
|---|---|---|
| Syllabus-relevant | 28 | ≈ 26 h |
| Skippable (Gap 3) | 12 | ≈ 11 h |
| Whole course | 40 | ≈ 37 h |

> Correction to my earlier estimate. I previously wrote "~20 of 40 lectures are on my syllabus." Recounting the mapping carefully gives 28, not 20, perfect graphs alone take five lectures (23–27) and network flows four (31–34). Corrected in [[NPTEL Index]].

---

## Suggested plan

1. This week. Lecture 02 (for the Hall half) and Lecture 03. Notes already written for both; watching closes the loop before Tutte begins.
2. Before the next class. Lectures 04–06 on Tutte, the next syllabus topic.
3. Ongoing, pick up each block as class reaches it, using the syllabus-order table above.
4. Separately, read West on the discharging method, since no video exists for it.

---

## All 40 direct links

Pulled from the playlist, in order.

| | Link | | Link |
|---|---|---|---|
| 01 | [Vertex Cover and Independent Set](https://www.youtube.com/watch?v=Gc8emFk-2vc) | 21 | [Chromatic Polynomial, k-Critical](https://www.youtube.com/watch?v=oFOPRPufisk) |
| 02 | [König's and Hall's Theorems](https://www.youtube.com/watch?v=IRbggk6J0TA) | 22 | [Gallai–Roy, Acyclic Colouring, Hadwiger](https://www.youtube.com/watch?v=OkgIaXhVVnc) |
| 03 | [More on Hall's Theorem](https://www.youtube.com/watch?v=BGCqWa33OD8) | 23 | [Perfect Graphs: Examples](https://www.youtube.com/watch?v=hJfHRbReGt4) |
| 04 | [Tutte's Theorem](https://www.youtube.com/watch?v=PM1FncPlXnM) | 24 | [Interval Graphs, Chordal Graphs](https://www.youtube.com/watch?v=Tg2_YO4CCNc) |
| 05 | [More on Tutte's Theorem](https://www.youtube.com/watch?v=_SOZz_aqRP4) | 25 | [Proof of the WPGT](https://www.youtube.com/watch?v=R1zyCMv03tk) |
| 06 | [More on Matchings](https://www.youtube.com/watch?v=7UZGUiG-UCw) | 26 | [Second Proof of WPGT](https://www.youtube.com/watch?v=OBp8klRZdDw) |
| 07 | [Dominating Set, Path Cover](https://www.youtube.com/watch?v=xi_f8TfH_qM) | 27 | [More Special Classes of Graphs](https://www.youtube.com/watch?v=TIeeu9aDifA) |
| 08 | [Gallai–Milgram, Dilworth](https://www.youtube.com/watch?v=1-NW2fKIyLQ) | 28 | [Boxicity, Sphericity, Hamiltonian Circuits](https://www.youtube.com/watch?v=n9FWAVIQ-oM) |
| 09 | [2-Connected and 3-Connected Graphs](https://www.youtube.com/watch?v=mNzg7CoF3r0) | 29 | [More on Hamiltonicity: Chvátal](https://www.youtube.com/watch?v=VugQE-SRHa0) |
| 10 | [Menger's Theorem](https://www.youtube.com/watch?v=4XC1tt80Eg8) | 30 | [Chvátal, Toughness, 4-Colour](https://www.youtube.com/watch?v=S1KgOr7sr6g) |
| 11 | [More on Connectivity: k-Linkedness](https://www.youtube.com/watch?v=eJmbXo1P6E4) | 31 | [Max-Flow Min-Cut](https://www.youtube.com/watch?v=Y9Ll0Ttfqzs) |
| 12 | [Minors, Topological Minors](https://www.youtube.com/watch?v=6SP09ZdV9uQ) | 32 | [Network Flows: Circulations](https://www.youtube.com/watch?v=ghtFBZPRfxg) |
| 13 | [Vertex Colouring: Brooks](https://www.youtube.com/watch?v=dwR1R-L9HEU) | 33 | [Circulations and Tensions](https://www.youtube.com/watch?v=VmnzH3GZiKw) |
| 14 | [More on Vertex Colouring](https://www.youtube.com/watch?v=EfZs9VDYeiU) | 34 | [Flow Number, Tutte's Flow Conjectures](https://www.youtube.com/watch?v=VuMVg1-QPhc) |
| 15 | [Edge Colouring: Vizing](https://www.youtube.com/watch?v=Ea3DlCoc0NQ) | 35 | [Random Graphs: Preliminaries](https://www.youtube.com/watch?v=wrskjcV7cW0) |
| 16 | [Vizing's Proof, Planarity](https://www.youtube.com/watch?v=TBYNkgvnU2s) | 36 | [Markov's Inequality, Ramsey](https://www.youtube.com/watch?v=BM24sU2Xm7w) |
| 17 | [5-Colouring Planar, Kuratowski](https://www.youtube.com/watch?v=kubJIJMOS8I) | 37 | [High Girth, High Chromatic Number](https://www.youtube.com/watch?v=XRaDIbBAb98) |
| 18 | [Kuratowski's Proof, List Colouring](https://www.youtube.com/watch?v=vEmogts6yg0) | 38 | [Second Moment, Lovász Local Lemma](https://www.youtube.com/watch?v=of3sPOMJb2I) |
| 19 | [List Chromatic Index](https://www.youtube.com/watch?v=GAlD0t25LYI) | 39 | [Graph Minors, Hadwiger](https://www.youtube.com/watch?v=ZD3Ai0BHYAQ) |
| 20 | [Adjacency Polynomial, Nullstellensatz](https://www.youtube.com/watch?v=DliIdpEWSTE) | 40 | [Graph Minors, Tree Decompositions](https://www.youtube.com/watch?v=zZbkLIWoIjc) |

Bold = on my syllabus and coming up. Lectures 01–05 are the ones covering class material so far.

## Sources

- [Playlist — Computer: Graph Theory (nptelhrd)](https://www.youtube.com/playlist?list=PL612CE2AB6F38DF9A)
- [NPTEL course 106108054](https://nptel.ac.in/courses/106108054)
- [Lecture titles and durations](https://freevideolectures.com/course/3019/graph-theory)
