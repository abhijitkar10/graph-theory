# Graph Theory — Course Notes

Worked notes for an advanced graph theory course, following **Diestel, *Graph Theory* (2nd ed.)**, with supplementary material from West and the NPTEL video course by Dr. L. Sunil Chandran (IISc Bangalore).

Every theorem here is **proved in full**. Proofs are broken into numbered sub-claims, each established separately and then combined — the aim is that nothing requires a leap.

---

## Start here

**[Master Notes](Master%20Notes.md)** — everything organised by *concept dependency* rather than by the date it was taught. Ten levels, a dependency map, a complete index of every result, and bridge sections filling gaps the lectures skipped.

If you want a specific proof, the master file tells you which note holds it.

---

## Class notes

Read in this order (the numbers matter — filenames sort differently):

| # | Note | Covers |
|---|---|---|
| 1 | [Preliminaries](2026-07-24%20Preliminaries.md) | cliques, edge density, minimum-degree subgraphs, maximal vs longest paths, trees, bipartite graphs |
| 2 | [Long Path Theorem](2026-07-24%20Long%20Path%20Theorem.md) | every connected graph has a path of length ≥ min{2δ, n−1}, proved in six claims |
| 3 | [Euler Circuits](2026-07-27%20Euler%20Circuits.md) | trails, circuits, components, Euler's theorem with both lemmas, Königsberg |
| 4 | [Euler by Extremal Argument, Matchings, MIS in Trees](2026-07-29%20Euler%20by%20Extremal%20Argument%2C%20Matchings%2C%20MIS%20in%20Trees.md) | a second, shorter proof of Euler via maximal trails; maximum independent sets in trees |
| 5 | [Matchings 2 — Berge and König](2026-07-29%20Matchings%202%20%E2%80%94%20Berge%20and%20K%C3%B6nig.md) | augmenting paths, Berge's theorem, ν ≤ τ ≤ 2ν, König's theorem |
| 6 | [Tutorial 1](Tutorial%201.md) | hypercubes and planarity, girth bounds, induced paths, the Helly property |

## Problem sets

- **[Assignment 1](Assignment%201.md)** — all 23 exercises from Diestel Chapter 1, worked in full

## NPTEL video-course notes

- [Index](nptel/NPTEL%20Index.md) — all 40 lectures mapped to syllabus topics
- [Course Resources](nptel/Course%20Resources.md) — what written material exists online
- [Lecture 01 — Vertex Cover and Independent Set](nptel/Lec%2001%20%E2%80%94%20Vertex%20Cover%20and%20Independent%20Set.md)
- [Lecture 02 — König's Theorem and Hall's Theorem](nptel/Lec%2002%20%E2%80%94%20K%C3%B6nig%27s%20Theorem%20and%20Hall%27s%20Theorem.md)
- [Lecture 03 — Hall's Theorem and Applications](nptel/Lec%2003%20%E2%80%94%20More%20on%20Hall%27s%20Theorem%20and%20Applications.md)

---

## Some results proved here

Konig's theorem · Hall's marriage theorem and its defect version · Berge's theorem · Euler's theorem (two independent proofs) · the long-path theorem · Moore bounds from girth · the four characterisations of a tree · greedy algorithms on trees justified by exchange arguments · the Helly property for intervals · why Q₄ is not planar.

## Two notes on reading these

**Written in Obsidian.** Cross-references use `[[wiki-link]]` syntax, which GitHub renders as plain text rather than as a link. Everything is still readable, but if you clone the folder into an Obsidian vault the cross-links become navigable.

**Equations use LaTeX** (`$...$` and `$$...$$`). GitHub renders these natively; some other markdown viewers do not.

---

*Notes prepared with the help of Claude. Errors are mine — corrections welcome via an issue.*
