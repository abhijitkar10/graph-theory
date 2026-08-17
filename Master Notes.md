---
tags: [academics, graph-theory, master, moc]
type: master
---

# Master Notes — Graph Theory by Concept Level

**Hub:** [[Graph Theory]]

> **What this file is.** Every definition, lemma, claim and exercise from all my notes, reorganised **by what depends on what** instead of by the date it was taught. Class notes follow the timeline; this follows the *logic*.
>
> **Bridges.** Where the notes jump over something, this file fills the gap with a short section marked **🌉 BRIDGE**. Those are concepts used but never formally defined anywhere else.
>
> **How to study with it.** Work down a level at a time. Don't start Level N until Level N−1 feels solid — each level genuinely uses the one before it.

---

## Dependency map

```
 L0  Vocabulary ──────────────┐
      │                       │
 L1  Walks, paths, distance   │
      │           │           │
 L2  EXTREMAL     └──► L3  Counting & density
      METHOD               │
      │  │                 │
      │  └──► L4  Trees ◄──┘
      │           │
      │      L5  Bipartite
      │           │
      ├──────► L6  Euler traversal
      │           │
      └──────► L7  Covering & packing (matchings)
                  │
              L8  Connectivity ──► L9  Planarity
                  │
              L10 The road ahead
```

**Read the arrows as "you need this first."** The two spines of the whole subject are **L2 (the extremal method)** and **L3 (counting)** — nearly every proof past that point is one of those two dressed up.

---

## Level index

| Level | Title | Status |
|---|---|---|
| **0** | Vocabulary — what a graph even is | ✅ solid |
| **1** | Walking around a graph | ✅ solid |
| **2** | ★ The extremal method | ✅ solid — **the key technique** |
| **3** | Counting and density arguments | ✅ solid |
| **4** | Trees | ✅ solid |
| **5** | Bipartite graphs | ✅ solid |
| **6** | Traversal — Euler circuits | ✅ solid |
| **7** | Covering and packing — matchings | 🟡 in progress (Tutte next) |
| **8** | Connectivity | 🟡 scattered results only |
| **9** | Planarity | 🔴 only touched once |
| **10** | The road ahead | 🔴 not started |

---

# LEVEL 0 — Vocabulary

**Prerequisites:** none.
**Why it exists:** almost every mistake I've made so far has been a *definition* mistake, not a proof mistake.

## The objects

| Term | Meaning | Source |
|---|---|---|
| **simple graph** | no self-loops, no repeated edges. Consequence used constantly: **v ∉ N(v)** | [[2026-07-24 Preliminaries]] §0 |
| **u ~ v** | u is adjacent to v | [[2026-07-24 Preliminaries]] §0 |
| **N(v)** | the neighbourhood — the set of vertices adjacent to v | [[2026-07-24 Preliminaries]] §0 |
| **N(S)** for a set S | vertices **outside S** with a neighbour in S | [[Lec 02 — König's Theorem and Hall's Theorem]] §0 |
| **N[v]** | the *closed* neighbourhood, {v} ∪ N(v) | [[Assignment 1]] Q10 |
| **deg(v)** | how many edges touch v | [[2026-07-24 Preliminaries]] §0 |
| **n, m** | number of vertices / edges | [[2026-07-24 Preliminaries]] §0 |
| **clique** | pairwise-adjacent set — a Kᵣ sitting inside G | [[2026-07-24 Preliminaries]] §1 |
| **independent set** | a set with **no** edges inside it | [[Lec 01 — Vertex Cover and Independent Set]] §1 |
| **complement Ḡ** | same vertices, edges exactly where G has none | [[Lec 01 — Vertex Cover and Independent Set]] §2 |

## Degree parameters

| Symbol | Meaning | Source |
|---|---|---|
| **δ(G)** | minimum degree *(my problem sheets sometimes write D(G) — same thing)* | [[2026-07-24 Preliminaries]] §0 |
| **Δ(G)** | maximum degree | [[2026-07-24 Preliminaries]] §0 |
| **average degree** | 2m/n | [[2026-07-24 Preliminaries]] §3 |
| **edge density ε(G)** | m/n = ½ × average degree | [[2026-07-24 Preliminaries]] §3 |
| **k-regular** | every vertex has degree exactly k | [[Lec 03 — More on Hall's Theorem and Applications]] §2 |

---

## 🌉 BRIDGE 0.1 — Subgraph, induced subgraph, spanning subgraph

*This is used everywhere — "induced path", "induced P₃", "subgraph H with δ(H) ≥ k" — but never actually defined in my notes. Fixing that here.*

> **Subgraph.** H is a **subgraph** of G if V(H) ⊆ V(G) and E(H) ⊆ E(G). You may delete vertices *and* delete edges freely.

> **Induced subgraph G[S].** Take a vertex set S ⊆ V(G) and keep **every edge of G with both ends in S**. You delete vertices, but you are **not allowed to drop edges** among the survivors. Written **G[S]**.

> **Spanning subgraph.** Keep **all** vertices (V(H) = V(G)) and delete only edges.

```
   G:  a———b        G[{a,b,c}] induced:  a———b      a subgraph (not induced):
       | \ |                             |   |          a———b
       c———d                             c———          |
                                        (edge ac kept — forced)     c
```

**Why the distinction matters, concretely:**

- **"Induced path"** (as in [[Tutorial 1]] Q3, Q5) means the path has **no chords**. The path a–b–c is an induced path only if ac is *absent from G*. If G happens to contain ac, then a–b–c is still a subgraph, but not an induced one.
- The greedy-deletion theorem of Level 3 produces an **induced** subgraph (we delete whole vertices, never individual edges).
- **Spanning** is the right word for trees inside a connected graph — a *spanning tree* keeps every vertex.

**Rule of thumb:** *induced = you don't get to choose which edges to ignore.* That's what makes induced-subgraph statements stronger and harder.

---

# LEVEL 1 — Walking around a graph

**Prerequisites:** Level 0.
**Why it exists:** four near-identical words that mean different things, and getting them wrong wrecks the Euler material.

## The four-way distinction

| Term | Repeated **vertices**? | Repeated **edges**? | Source |
|---|---|---|---|
| **walk** | ✓ allowed | ✓ allowed | [[2026-07-27 Euler Circuits]] §0 |
| **trail** | ✓ allowed | ✗ **forbidden** | [[2026-07-27 Euler Circuits]] §0 |
| **path** | ✗ forbidden | ✗ forbidden | [[2026-07-27 Euler Circuits]] §0 |
| **circuit** | ✓ allowed | ✗ forbidden, **and closed** | [[2026-07-27 Euler Circuits]] §0 |

> **Length** always means the **number of edges**. A path on m vertices has length m−1. This trips me up constantly.

## Connectivity and components

| Result | Statement | Source |
|---|---|---|
| **component** | a maximal connected subgraph | [[2026-07-27 Euler Circuits]] §0 |
| **trivial component** | a single isolated vertex (no edges) | [[2026-07-27 Euler Circuits]] §0 |
| Components **partition** V(G) | every vertex lies in exactly one | [[Assignment 1]] Q11 |

## Distance parameters

| Symbol | Meaning | Source |
|---|---|---|
| **d(u,v)** | length of a shortest u–v path | [[Assignment 1]] Q5 |
| **eccentricity ecc(v)** | distance to the furthest vertex from v | [[Assignment 1]] Q6 |
| **radius / diameter** | min / max of the eccentricities | [[Assignment 1]] Q6 |
| **girth** | length of the **shortest** cycle | [[Assignment 1]] Q2 |
| **circumference** | length of the **longest** cycle | [[Assignment 1]] Q2 |

| Result | Statement | Source |
|---|---|---|
| **rad ≤ diam ≤ 2·rad** | route everything through a centre | [[Assignment 1]] Q6 |
| **Distance layers** | Dₙ = {v : d(v₀,v) = n}; edges never skip a layer | [[Assignment 1]] Q5 |
| **Shortest ⇒ induced** | a shortest path has no chords | [[Tutorial 1]] Q5 |
| **Not complete + connected ⇒ induced P₃** | take the first 3 vertices of a shortest path | [[Tutorial 1]] Q3 |
| **girth ≤ 2·diam + 1** | tight at odd cycles | [[Assignment 1]] Q4 |

---

## 🌉 BRIDGE 1.1 — Every walk contains a path

*Used silently in [[Assignment 1]] Q11 to prove transitivity. Worth stating properly because it's the reason you can be sloppy about walks vs paths when you only care about **reachability**.*

> **Lemma.** If there is a u–v **walk**, then there is a u–v **path**.

**Proof.** Take a u–v walk W with the **fewest edges** *(an extremal choice — Level 2 in miniature)*.

Suppose W repeats a vertex x, visiting it at two different times. Cut out the entire loop between those two visits. What remains is still a u–v walk — you leave x and re-enter the route at x — and it is **strictly shorter** ✗ contradicting minimality.

So W repeats no vertex, i.e. W **is** a path ∎

**Why it matters:** "u and v are in the same component" can be checked with *any* walk, however messy. You never have to be careful about repeats when the only question is *can I get there*.

---

# LEVEL 2 — ★ The extremal method

**Prerequisites:** Levels 0–1.
**Why it exists:** **this is the single most important technique in the course so far.** Nine separate results below are the same idea.

> **The method.** Choose an object that is **extreme** in some way — longest, maximal, minimal, largest index, rightmost endpoint. Then ask: *what does the fact that it cannot be improved force to be true?* The answer is usually the whole proof.

## Maximal vs longest — get this straight first

| | **maximal** | **longest / maximum** |
|---|---|---|
| meaning | **cannot be extended** | no longer one exists anywhere |
| finding it | greedy — walk until stuck | search everything |
| cost | **polynomial** | **NP-complete** |

Source: [[2026-07-24 Preliminaries]] §5.

> **Crucial:** every proof below only needs "**can't be extended**", so **maximal** always suffices. That's a much cheaper object, and one always exists.

## The trapped-endpoint principle

> Take a **maximal path** P. Its **two endpoints are trapped** — every one of their neighbours already lies on P, because an outside neighbour could be tacked on.

⚠️ **Only the endpoints.** Interior vertices are free — you can only extend a path at its ends. → [[2026-07-24 Long Path Theorem]] Claim 1.

## Everything that falls out of it

| Result | Statement | Source |
|---|---|---|
| **Lemma A** | δ ≥ k ⇒ a path with ≥ k+1 vertices | [[2026-07-24 Preliminaries]] §6 |
| **Lemma B** | δ ≥ 2 ⇒ G contains a **cycle** | [[2026-07-24 Preliminaries]] §6 |
| **Lemma C** | δ ≥ k ⇒ a cycle of length ≥ k+1 | [[2026-07-24 Preliminaries]] §6 |
| **Even cycle** | δ ≥ 3 ⇒ an **even** cycle exists | [[2026-07-24 Preliminaries]] §7 |
| ★ **Long-path theorem** | connected ⇒ path of length ≥ min{2δ, n−1} | [[2026-07-24 Long Path Theorem]] |
| ★ **Path-or-cycle** | connected ⇒ path **or cycle** of length ≥ min{2δ, n} | [[Assignment 1]] Q9 |
| **Two longest paths meet** | any two longest paths share a vertex | [[Tutorial 1]] Q4 |
| **Maximal trail ⇒ Euler** | a maximal trail is closed and uses every edge | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] |
| **Greedy deletion** | strip low-degree vertices until stuck | [[2026-07-24 Preliminaries]] §4 |
| **Helly (1-D)** | take the **rightmost** left endpoint | [[Tutorial 1]] Q6 |
| **Walk contains path** | take the shortest walk | 🌉 Bridge 1.1 above |

## The supporting moves

These small tools show up *inside* extremal proofs:

| Move | What it says | Where |
|---|---|---|
| **Pigeonhole** | two sets in a box of size k with sizes summing past k must overlap | [[2026-07-24 Long Path Theorem]] Claim 3 |
| **Fold a path into a cycle** | two *crossing* edges (offset by one) close the loop | [[2026-07-24 Long Path Theorem]] Claim 4 |
| **Snip and extend** | reopening a cycle frees an endpoint you can grow | [[2026-07-24 Long Path Theorem]] Claim 6 |
| **"Shortest forbids shortcuts"** | a chord would contradict minimality | [[Tutorial 1]] Q3, Q5 |
| **Exchange argument** | modify *any* optimum to agree with your greedy choice | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] Claim 4 |
| **Symmetric difference** | M △ M′ has max degree 2 ⇒ splits into paths and cycles | [[Lec 02 — König's Theorem and Hall's Theorem]] §2 |
| **Parity** | odd + odd = even, so three quantities can't all be odd | [[2026-07-24 Preliminaries]] §7 |

---

# LEVEL 3 — Counting and density

**Prerequisites:** Levels 0–1. Independent of Level 2 — a *second* spine.
**Why it exists:** the other half of every proof. When extremality doesn't crack it, count something two ways.

## Handshake lemma — the root of everything here

$$\sum_{v} \deg(v) = 2m$$

**Why:** count (vertex, edge-touching-it) pairs two ways. Source: [[2026-07-24 Preliminaries]] §3.

---

## 🌉 BRIDGE 3.1 — The parity corollary of handshake

*Never stated in my notes, but it is the cleanest way to see why Euler's theorem looks the way it does.*

> **Corollary.** In **every** graph, the number of vertices of **odd degree** is **even**.

**Proof.** Split the handshake sum by parity:

$$\underbrace{\sum_{\deg \text{ even}} \deg(v)}_{\text{a sum of even numbers} \;\Rightarrow\; \text{even}} \;+\; \sum_{\deg \text{ odd}} \deg(v) \;=\; \underbrace{2m}_{\text{even}}$$

Subtracting, the odd-degree sum must itself be **even**. But it is a sum of **odd** numbers — and a sum of odd numbers is even exactly when there is an **even count** of them ✓ ∎

**Numbers.** A path a–b–c: degrees 1, 2, 1 → two odd vertices ✓ A triangle: 2, 2, 2 → zero odd ✓ You can never build a graph with exactly one odd-degree vertex.

**Why this bridges to Euler.** [[2026-07-27 Euler Circuits]] shows an Euler circuit needs *all* degrees even. This corollary explains the *next* question — an Euler **trail** (open, different start and end) needs exactly **two** odd vertices, and by the corollary you can never have just one. That's why the theory splits into "0 odd vertices → circuit" and "2 odd vertices → open trail", with no other possibility.

*Königsberg had **four** odd vertices, which kills both.*

---

## Density results

| Result | Statement | Source |
|---|---|---|
| **ε(G) = ½ × avg degree** | edge density and average degree are the same fact | [[2026-07-24 Preliminaries]] §3 |
| **m > C(n−1,2) ⇒ connected** | sharp — Kₙ₋₁ plus isolated vertex sits exactly at the threshold | [[2026-07-24 Preliminaries]] §2 |
| ★ **Density k ⇒ subgraph with δ ≥ k** | greedy deletion; density *rises* as you strip | [[2026-07-24 Preliminaries]] §4 |
| **e(G) > k(n−1) ⇒ (k+1)-edge-connected subgraph** | minimal-subgraph argument | [[Assignment 1]] Q16 |
| **Smallest b(k)** | −k(k+1)/2 ≤ b(k) ≤ −k; exact at b(1) = −1 | [[Assignment 1]] Q18 |

---

## 🌉 BRIDGE 3.2 — That greedy-deletion theorem has a name: **degeneracy**

*This is on my syllabus as its own topic ("degeneracy of graphs"), and I've already proved the main fact without knowing the name. Connecting them now.*

> **Definition.** G is **d-degenerate** if **every** subgraph of G has a vertex of degree ≤ d. The **degeneracy** of G is the smallest such d.

**The link:** [[2026-07-24 Preliminaries]] §4 proves that if every subgraph *failed* to have a low-degree vertex, you could strip forever. Restated:

> G is d-degenerate **⟺** the greedy "repeatedly delete a vertex of degree ≤ d" procedure empties the graph.

That procedure produces a **degeneracy ordering** v₁, v₂, …, vₙ — the reverse of the deletion order — in which every vertex has **at most d** neighbours *earlier* than itself.

**Why I'll care later (colouring, Level 10):** feed a degeneracy ordering to greedy colouring. Each vertex sees ≤ d already-coloured neighbours, so d+1 colours always suffice:

$$\chi(G) \;\le\; \text{degeneracy}(G) + 1.$$

**Numbers.** Every **tree** is 1-degenerate (every subgraph has a leaf → Level 4), so χ(tree) ≤ 2 ✓ correct, trees are bipartite. Every **planar** graph is 5-degenerate, giving the 6-colour theorem for free.

So Level 3's greedy deletion and the syllabus's "degeneracy" and "greedy colouring" are **one idea seen three times**.

---

## Girth forces room

Both of these are the same count — {v} ∪ N(v) ∪ (outer neighbours), forced disjoint by the absence of short cycles.

| Result | Statement | Source |
|---|---|---|
| **girth ≥ 5 ⇒ δ ≤ √(n−1)** | fix n, degree is capped | [[Assignment 1]] Q8 |
| **k-regular, girth 5 ⇒ n ≥ k²+1** | fix degree, size is forced up. **Tight**: Petersen, C₅ | [[Tutorial 1]] Q2 |
| **Moore bound** | δ ≥ d, girth ≥ g ⇒ n ≥ n₀(d,g) | [[Assignment 1]] Q7 |
| **diam k, min degree d ⇒ ≈ kd/3 vertices** | grab every **third** vertex of a shortest path | [[Assignment 1]] Q10 |

> **The shared engine:** large girth means balls around a vertex are **trees** — no shortcuts — so each level multiplies by (d−1). Small girth is exactly what lets a graph be small *and* dense.

---

# LEVEL 4 — Trees

**Prerequisites:** Levels 0–3 (Lemma B from Level 2 is used to prove leaves exist).
**Why it exists:** trees are the boundary case between "too few edges to connect" and "enough edges to make a cycle" — and that tension is where all their properties come from.

> **Definition.** A **tree** is a **connected, acyclic** graph. A **forest** is any acyclic graph (a disjoint union of trees).

## The four characterisations — Theorem 1.5.1

All equivalent. → [[Assignment 1]] Q19.

| | Characterisation |
|---|---|
| **(1)** | connected and acyclic |
| **(2)** | any two vertices joined by a **unique** path |
| **(3)** | **minimally connected** — removing any edge disconnects |
| **(4)** | **maximally acyclic** — adding any edge creates a cycle |

> **The picture:** a tree is exactly the tipping point. Take an edge away and it falls apart (3); put one in and a cycle appears (4). Unique paths (2) is the same balance seen from the middle.

## Core facts

| Result | Statement | Source |
|---|---|---|
| **Leaf existence** | every tree with n ≥ 2 has a leaf — else δ ≥ 2 and Lemma B gives a cycle | [[2026-07-24 Preliminaries]] §8 |
| **Edge count** | a tree on n vertices has exactly **n−1** edges | [[2026-07-24 Preliminaries]] §8 |
| **Unique paths** | two distinct u–v paths would create a cycle | [[2026-07-24 Preliminaries]] §8 |
| **Forest edge count** | a forest with c components has **n − c** edges | [[Assignment 1]] Q22 |
| **≥ Δ(T) leaves** | delete a max-degree vertex; each of the Δ pieces yields a leaf | [[Assignment 1]] Q20 |
| **No degree-2 ⇒ L ≥ I + 2** | pure handshake, no induction | [[Assignment 1]] Q21 |
| **Forest exchange** | e(F) < e(F′) ⇒ some edge of F′ extends F | [[Assignment 1]] Q22 |
| **Tree-order** | x ≤ y iff x is on the root–y path; a partial order | [[Assignment 1]] Q23 |
| ★ **MIS by greedy on leaves** | take all leaves, delete their parents, recurse | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] |
| ★ **MIS by tree DP** | MIS(v,0) = Σ max{MIS(u,0), MIS(u,1)}; MIS(v,1) = 1 + Σ MIS(u,0). O(n) | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] |
| **Level-splitting fails** | max{odd levels, even levels} is *not* the MIS | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] |
| **Leaf's parent** | lies in **every** maximum matching of a tree | [[2026-08-10 Matchings in Bipartite Graphs]] §2 |
| **Matching in a tree** | anywhere from 1 (star) to ⌊n/2⌋; **no formula in terms of depth** | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] |

> **Connections outward:** trees are **1-degenerate** (Bridge 3.2) and **bipartite** (Level 5, colour by level parity). The forest exchange property is the **matroid** exchange axiom, which is why Kruskal's algorithm works.

---

# LEVEL 5 — Bipartite graphs

**Prerequisites:** Levels 0–2 (the even-cycle machinery), Level 4 for the tree example.
**Why it exists:** bipartiteness is the single hypothesis that turns several NP-hard problems polynomial. Knowing *exactly* what it means is worth a lot later.

> **Definition.** G is **bipartite** if V splits into two **independent sets** X and Y — every edge crosses, none lies inside a part. Equivalently: G can be **2-coloured** so no edge joins same-coloured vertices.

## The characterisation

> ★ **G is bipartite ⟺ G has no odd cycle.**

| Direction | Idea | Source |
|---|---|---|
| odd cycle ⇒ not bipartite | walking a cycle **alternates** sides, so closing up forces even length | [[2026-07-24 Preliminaries]] §9 |
| no odd cycle ⇒ bipartite | root it, split by **parity of d(r, ·)**; a bad edge would close an odd cycle | [[2026-07-24 Preliminaries]] §9 |
| ★ **connected ⇒ unique bipartition** | all r–v paths have the same parity, so every vertex's side is forced | [[2026-07-29 Matchings 2 — Berge and König]] §7 |

> ⚠️ Uniqueness **needs connectedness** — each component can be flipped independently, so two disjoint edges have four bipartitions.

> **The recurring trick:** *colour by a parity*. Level parity for trees, distance parity here, count-of-1s parity for the hypercube.

## Worked family — the hypercube Qₙ

→ [[Tutorial 1]] Q1 and [[Assignment 1]] Q2.

| Invariant | Value |
|---|---|
| vertices | 2ⁿ |
| degree | n (it is n-regular) |
| edges | n·2ⁿ⁻¹ |
| diameter | n (= Hamming distance) |
| girth | 4 (for n ≥ 2) |
| circumference | 2ⁿ — it is **Hamiltonian** |
| bipartite? | ✅ by **parity of the number of 1s** |
| planar? | Q₃ yes (exactly at the limit), **Q₄ no** |

## Consequences that need bipartiteness

| Result | Statement | Source |
|---|---|---|
| **König** | ν = τ in bipartite graphs | Level 7 |
| **Hall** | matching criterion | Level 7 |
| **k-regular bipartite** | has a perfect matching; splits into k of them | Level 7 |
| **Edge colouring** | bipartite needs exactly Δ colours, never Δ+1 | Level 7 |
| **Planarity bound** | bipartite planar ⇒ m ≤ 2n−4, stronger than 3n−6 | Level 9 |

---

# LEVEL 6 — Traversal: Euler circuits

**Prerequisites:** Level 1 (the trail/path vocabulary is *essential* here), Level 2 (both proofs are extremal or inductive), Bridge 3.1 (the parity corollary).

> **Euler circuit** = a circuit containing **every edge**. In plain terms: draw the whole graph in one pen stroke, never retracing, finishing where you started.

## ★ Euler's Theorem

> **G has an Euler circuit ⟺ G has at most one non-trivial component AND every vertex has even degree.**

| Half | Name | Idea | Source |
|---|---|---|---|
| ⇒ | **Lemma 1** | each visit burns exactly **2** edges, so degrees pair up | [[2026-07-27 Euler Circuits]] |
| ⇐ | **Lemma 2** | two different proofs — see below | both notes |

## Two proofs of Lemma 2 — know both

| | **Induction on edges** | **Maximal trail (extremal)** |
|---|---|---|
| idea | pull out a cycle, recurse, splice back | take a trail you can't extend |
| difficulty | fiddly — deleting a cycle can **shatter** the graph, so you recurse per component and glue | clean — the graph is never split |
| source | [[2026-07-27 Euler Circuits]] | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] |

**The extremal proof in two claims:**

- **Claim 1** — a maximal trail is **closed**. An open trail uses an *odd* number of edges at its final endpoint (2 per pass-through, +1 for the last arrival), clashing with even degree.
- **Claim 2** — a maximal trail uses **every** edge. Being closed, it can be restarted anywhere, so any leftover edge touching it extends it.

## Using the theorem

**Contrapositive + De Morgan** — ¬(Q ∧ R) = ¬Q ∨ ¬R:

> More than one non-trivial component **OR** one odd-degree vertex ⇒ **no** Euler circuit.

The **OR** is the practical form: a *single* odd vertex kills it. Königsberg has four → the bridge tour is impossible. → [[2026-07-27 Euler Circuits]]

> ⚠️ **Isolated vertices are harmless** — an Euler circuit owes a visit to *edges*, not vertices. That's why the condition says "at most one **non-trivial** component" rather than "connected".

## The contrast that matters

| | **Euler circuit** | **Hamiltonian cycle** |
|---|---|---|
| covers | every **edge** once | every **vertex** once |
| test | easy — check degrees | **NP-complete** |
| status | fully solved | no efficient characterisation |

Two near-mirror questions on opposite sides of the tractability line. → [[2026-07-27 Euler Circuits]]

---

# LEVEL 7 — Covering and packing (matchings)

**Prerequisites:** Levels 0–5. This is where the syllabus proper begins.
**Why it exists:** four parameters that pair up into two identities, one inequality that bipartiteness turns into an equality, and a criterion (Hall) that generates a dozen applications.

## The four parameters

| Symbol | Name | Max or min? | Source |
|---|---|---|---|
| **α(G)** | independence number | **max** | [[Lec 01 — Vertex Cover and Independent Set]] |
| **τ(G)** | vertex cover number | **min** | [[Lec 01 — Vertex Cover and Independent Set]] |
| **ν(G)** | matching number | **max** | [[Lec 01 — Vertex Cover and Independent Set]] |
| **ρ(G)** | edge cover number | **min** | [[Lec 01 — Vertex Cover and Independent Set]] |

> **Mnemonic:** α and ν are what you **maximise**; τ and ρ what you **minimise**. Subscript-free α/τ are about **vertices**, ν/ρ about **edges**.

```
            packing (max)      covering (min)
 vertices     α                  τ            α + τ = n
 edges        ν                  ρ            ν + ρ = n
```

## The identities and the inequality

| Result | Statement | Source |
|---|---|---|
| **S independent ⟺ V∖S a cover** | one set, two names | [[Lec 01 — Vertex Cover and Independent Set]] §2 |
| **Gallai I** | α + τ = n | [[Lec 01 — Vertex Cover and Independent Set]] §2 |
| **Gallai II** | ν + ρ = n (no isolated vertices) | [[Lec 01 — Vertex Cover and Independent Set]] §4 |
| **α(G) = ω(Ḡ)** | independent set = clique in the complement | [[Lec 01 — Vertex Cover and Independent Set]] §2 |
| ★ **ν ≤ τ** | matching edges are disjoint, each needs its own cover vertex | [[Lec 01 — Vertex Cover and Independent Set]] §3 |
| **ν ≤ ⌊n/2⌋** | a matching uses 2ν distinct vertices | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] |
| ★ **τ ≤ 2ν** | take **both** endpoints of a maximum matching — that set covers everything | [[2026-07-29 Matchings 2 — Berge and König]] §5 |

> ★ **The sandwich ν ≤ τ ≤ 2ν.** Lower half tight for every bipartite graph (König); upper half tight at **K₃** and disjoint triangles. The upper half *is* the standard **2-approximation** for the NP-hard vertex cover problem.

**Values worth memorising** *(note τ = n − α throughout — Gallai)*:

| Graph | ν | α | τ = n − α | ν = τ? |
|---|---|---|---|---|
| Pₙ | ⌊n/2⌋ | ⌈n/2⌉ | ⌊n/2⌋ | ✅ |
| Cₙ | ⌊n/2⌋ | ⌊n/2⌋ | ⌈n/2⌉ | ✅ n even · ❌ n odd |
| Star Sₙ | 1 | n−1 | 1 | ✅ |
| Kₙ | ⌊n/2⌋ | 1 | n−1 | ❌ (n ≥ 3) |
| Tree | k | n−k | k | ✅ |
| K_{k,l} | min(k,l) | max(k,l) | **min(k,l)** | ✅ |

> **Read the last column:** equality exactly for the **bipartite** ones. That pattern *is* König.

> **K₃ is the minimal witness of ν < τ** (1 < 2) — and K₃ is the smallest odd cycle. That is *exactly* why König needs bipartiteness.

## Augmenting paths

| Result | Statement | Source |
|---|---|---|
| **alternating / augmenting path** | alternates in/out of M; augmenting = both ends unmatched | [[Lec 02 — König's Theorem and Hall's Theorem]] §1 |
| ★ **Berge** | M is maximum **⟺** no M-augmenting path | [[Lec 02 — König's Theorem and Hall's Theorem]] §2 · [[2026-07-29 Matchings 2 — Berge and König]] §4 |
| **M ∪ N has Δ ≤ 2** | so it splits into alternating **paths and even cycles** — the engine of Berge's hard direction | [[2026-07-29 Matchings 2 — Berge and König]] Claim 2.2 |
| **Augmenting algorithm** | while an augmenting path exists, take M △ P; halts in ≤ ⌊n/2⌋ rounds | [[2026-07-29 Matchings 2 — Berge and König]] §4 |
| **Leaf edge is safe** | a leaf's edge lies in *some* maximum matching (exchange argument) | [[2026-07-29 Matchings 2 — Berge and König]] §2 |

> **Why Berge matters:** it turns "is this optimal?" into a **search**. Every matching algorithm hunts augmenting paths.

## The two big theorems

| Result | Statement | Source |
|---|---|---|
| ★ **König** | **bipartite** ⇒ ν = τ | [[Lec 02 — König's Theorem and Hall's Theorem]] §3 · [[2026-07-29 Matchings 2 — Berge and König]] §6 |
| **min{\|A\|,\|B\|}** | only an **upper bound** on τ; equality needs **complete** bipartite | [[2026-07-29 Matchings 2 — Berge and König]] §7 |
| ★ **Hall** | a matching saturates A ⟺ \|N(S)\| ≥ \|S\| for all S ⊆ A | [[Lec 02 — König's Theorem and Hall's Theorem]] §4 |
| **König ⟺ Hall** | each is a two-line consequence of the other | [[Lec 02 — König's Theorem and Hall's Theorem]] §5 |
| ★ **Defect Hall** | ν = \|A\| − max deficiency | [[Lec 03 — More on Hall's Theorem and Applications]] §1 |
| ★ **Universal vertex** | bipartite ⇒ some vertex lies in **every** maximum matching | [[2026-08-10 Matchings in Bipartite Graphs]] §3 |
| **≥ τ universal vertices** | bipartite ⇒ at least \|MVC\| of them, by peeling one off and inducting | [[2026-08-10 Matchings in Bipartite Graphs]] §4 |

> ★ **Odd cycles are the sole obstruction.** The universal-vertex proof is valid for *any* graph right up to its final step, where it produces an odd cycle. C₂ₙ₊₁ is vertex-transitive, so every vertex is missed by some maximum matching — verified: C₃, C₅, C₇, C₉ each have **zero** universal vertices, while even cycles have all n.

> **Parity of the swap — the distinction to hold on to.** Swapping along an **odd** alternating path **gains** an edge (Berge, §augmenting). Swapping along an **even** one **preserves** size — which is exactly what makes the universal-vertex proof work. Same operation, opposite purposes.

## Applications of Hall

All follow one template: *build a bipartite graph where the thing you want is a perfect matching, then verify Hall — usually via regularity.*

| Result | Statement | Source |
|---|---|---|
| **k-regular bipartite ⇒ perfect matching** | count edges out of S two ways | [[Lec 03 — More on Hall's Theorem and Applications]] §2 |
| **⇒ k disjoint perfect matchings** | peel one off, the rest stays regular | [[Lec 03 — More on Hall's Theorem and Applications]] §3 |
| **SDRs** | Hall relabelled: indices vs elements | [[Lec 03 — More on Hall's Theorem and Applications]] §4 |
| **Latin rectangle extends** | "still-free symbols" is (n−r)-regular | [[Lec 03 — More on Hall's Theorem and Applications]] §5 |
| **Birkhoff–von Neumann** | doubly stochastic = convex combination of permutations | [[Lec 03 — More on Hall's Theorem and Applications]] §6 |

## Complexity payoff

| Problem | General | Bipartite |
|---|---|---|
| max matching ν | polynomial (Edmonds) | polynomial |
| min vertex cover τ | **NP-hard** | polynomial — via König |
| max independent set α | **NP-hard** | polynomial — via α = n − τ |

---

## 🌉 BRIDGE 7.1 — The min-max duality family

*My notes keep saying "these are all the same theorem" without laying it out. Here it is.*

A **min-max theorem** says *the largest packing equals the smallest blocker*. Five results on my syllabus have that shape, and each implies the others:

| Theorem | max thing | = | min thing | Status |
|---|---|---|---|---|
| **König** | matching ν | = | vertex cover τ | ✅ Level 7 |
| **Hall** | *(feasibility form of König)* | | | ✅ Level 7 |
| **Menger** | disjoint u–v paths | = | u–v separating set | 🔜 Level 8 |
| **Max-flow min-cut** | flow value | = | cut capacity | 🔜 Level 10 |
| **Dilworth** | antichain | = | chain cover | 🔜 (NPTEL Lec 08) |
| **Tutte** | *(feasibility form for general matchings)* | | | 🔜 next class |

**The pattern to carry:** every one of these has an **easy direction** (max ≤ min — any packing is blocked by any blocker, one item at a time) and a **hard direction** (equality — you must *construct* an optimal blocker from an optimal packing).

In König the construction was **alternating reachability from the unmatched vertices**. Expect Menger's proof to do something structurally identical. When I get there, the question to ask is: *what plays the role of the alternating path?*

> **Feasibility vs min-max.** Hall and Tutte are *feasibility* statements ("a perfect assignment exists iff…"), König and Menger are *min-max* statements. They're two faces of one result — the feasibility version is what you get by asking when the min-max quantity hits its ceiling.

---

# LEVEL 8 — Connectivity

**Prerequisites:** Levels 0–4, 7.
**Status:** 🟡 I have scattered results but the **theory** (Menger, ear decomposition) is still ahead.

| Symbol | Meaning |
|---|---|
| **κ(G)** | vertex connectivity — fewest vertices whose removal disconnects |
| **λ(G)** | edge connectivity — fewest edges |

> **The chain: κ(G) ≤ λ(G) ≤ δ(G).** Vertices are at least as powerful as edges, and killing one vertex's edges always disconnects it.

| Result | Statement | Source |
|---|---|---|
| **2-connected ⇒ has a cycle** | 2-connected forces δ ≥ 2, then Lemma B | [[Assignment 1]] Q12 |
| **κ, λ of standard families** | Pᵐ:1,1 · Cⁿ:2,2 · Kⁿ:n−1 · Kᵐ˒ⁿ:min(m,n) · Qₙ:n | [[Assignment 1]] Q13 |
| **Min degree can't force k-connectivity** | glue two huge cliques at one cut vertex | [[Assignment 1]] Q14 |
| **But density forces edge-connected subgraphs** | e > k(n−1) ⇒ (k+1)-edge-connected subgraph | [[Assignment 1]] Q16 |
| **Invariant formalism** | "bounded by a function of" ⟺ "can be forced up by" | [[Assignment 1]] Q15 |

> **The lesson of Q14 vs Q16:** minimum degree is **local**, connectivity is **global**, so local hypotheses can never force global connectivity of the *whole* graph — but they *can* force it on a **subgraph**. Passing to a subgraph is the move that rescues the idea.

**Still ahead:** Menger's theorem, Dirac's extensions, ear decomposition, structure of minimum cuts.

---

# LEVEL 9 — Planarity

**Prerequisites:** Levels 0–5.
**Status:** 🔴 touched exactly once, for Q₄. Needs building out.

## 🌉 BRIDGE 9.1 — Euler's formula, which I used without proving

*[[Tutorial 1]] Q1 uses the bound m ≤ 2n−4 and derives it from Euler's formula — but the formula itself was never justified. Filling that in.*

> **Euler's formula.** For a **connected plane** graph (drawn with no crossings), with n vertices, m edges and **f faces**:
> $$n - m + f = 2$$

**Proof sketch by induction on m.**

- **Base:** a **tree** has m = n−1 and only the outer face, f = 1. Then n − (n−1) + 1 = 2 ✓
- **Step:** if G is not a tree it has a cycle. Delete one cycle edge. That edge separated two distinct faces, which now **merge**: m drops by 1, f drops by 1, n unchanged — so n − m + f is unchanged ✓ Repeat until a tree remains ∎

### The two counting bounds

Both come from *"each face needs enough edges, and each edge serves at most 2 faces."*

| Assumption | Face bound | Result |
|---|---|---|
| simple, n ≥ 3 | every face has ≥ **3** edges ⇒ 3f ≤ 2m | **m ≤ 3n − 6** |
| **bipartite**, n ≥ 3 | no triangles, so every face has ≥ **4** ⇒ 4f ≤ 2m | **m ≤ 2n − 4** |

**Derivation of the bipartite one** (the version I actually needed): from 4f ≤ 2m we get f ≤ m/2, so

$$2 = n - m + f \le n - m + \tfrac{m}{2} = n - \tfrac{m}{2} \quad\Longrightarrow\quad m \le 2n-4 \;✓$$

### Applied

| Graph | n | m | 3n−6 | 2n−4 | Planar? |
|---|---|---|---|---|---|
| K₅ | 5 | 10 | **9** | — | ❌ 10 > 9 |
| K₃,₃ | 6 | 9 | 12 | **8** | ❌ 9 > 8 (needs bipartite bound) |
| Q₃ | 8 | 12 | 18 | **12** | ✅ exactly at the limit |
| **Q₄** | 16 | 32 | 42 | **28** | ❌ 32 > 28 |

> ⚠️ **The trap I must remember:** for Q₄ and K₃,₃ the general 3n−6 bound is **too weak** and says nothing. You must use the bipartite 2n−4. Checking bipartiteness first is the habit to build.

**K₅ and K₃,₃ matter** because Kuratowski's theorem (ahead) says they are the *only* obstructions — a graph is planar iff it contains no subdivision of either.

**Still ahead:** Kuratowski's theorem, 5-colouring planar graphs, the discharging method.

---

# LEVEL 10 — The road ahead

Everything on my syllabus not yet reached, in dependency order.

| Topic | Needs | NPTEL | Notes |
|---|---|---|---|
| **Tutte's theorem** | Level 7 | Lec 04–06 | 🔜 next class |
| **2-connected, ear decomposition** | Level 8 | Lec 09 | |
| **Menger's theorem** | Level 8, Bridge 7.1 | Lec 10 | the min-max pattern repeats |
| **Dirac's extensions** | Menger | Lec 11 | |
| **Vertex colouring, greedy, degeneracy** | Bridge 3.2 | Lec 13–14 | *I've already proved the core fact* |
| **Brooks' theorem** | greedy colouring | Lec 13 | |
| **Edge colouring, König, Vizing** | Level 7 | Lec 15–16 | bipartite case already done |
| **Planar colouring** | Level 9 | Lec 17 | |
| **Perfect graphs** | Levels 5, 7 | Lec 23–27 | |
| **Hamiltonian graphs** | Level 6 contrast | Lec 28–30 | |
| **Ramsey theory** | Level 3 counting | Lec 36 | |
| **Network flows, min cuts** | Bridge 7.1 | Lec 31–34 | max-flow min-cut ⇒ König |
| **Discharging method** | Level 9 | ❌ **not in NPTEL** | must come from **West** |

---

# Complete index of results

Every named claim, lemma and theorem across all my notes, alphabetically.

| Result | Level | Where |
|---|---|---|
| Berge's theorem | 7 | [[Lec 02 — König's Theorem and Hall's Theorem]] · [[2026-07-29 Matchings 2 — Berge and König]] |
| Bipartite ⟺ no odd cycle | 5 | [[2026-07-24 Preliminaries]] §9 |
| Bipartition unique (connected) | 5 | [[2026-07-29 Matchings 2 — Berge and König]] §7 |
| Birkhoff–von Neumann | 7 | [[Lec 03 — More on Hall's Theorem and Applications]] |
| Components partition V | 1 | [[Assignment 1]] Q11 |
| Defect Hall | 7 | [[Lec 03 — More on Hall's Theorem and Applications]] |
| Degeneracy ↔ greedy deletion | 3 | 🌉 Bridge 3.2 |
| Density k ⇒ subgraph δ(H) ≥ k | 3 | [[2026-07-24 Preliminaries]] §4 |
| Diameter k + min degree d ⇒ ≈ kd/3 | 3 | [[Assignment 1]] Q10 |
| Distance layers | 1 | [[Assignment 1]] Q5 |
| Euler's formula n − m + f = 2 | 9 | 🌉 Bridge 9.1 |
| Euler's theorem (Lemmas 1 & 2) | 6 | [[2026-07-27 Euler Circuits]] |
| — Lemma 2 by maximal trail | 6 | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] |
| Forest exchange property | 4 | [[Assignment 1]] Q22 |
| Gallai I: α + τ = n | 7 | [[Lec 01 — Vertex Cover and Independent Set]] |
| Gallai II: ν + ρ = n | 7 | [[Lec 01 — Vertex Cover and Independent Set]] |
| girth ≤ 2·diam + 1 | 1 | [[Assignment 1]] Q4 |
| girth 5 ⇒ δ ≤ √(n−1) | 3 | [[Assignment 1]] Q8 |
| Hall's marriage theorem | 7 | [[Lec 02 — König's Theorem and Hall's Theorem]] |
| Handshake lemma | 3 | [[2026-07-24 Preliminaries]] §3 |
| — parity corollary | 3 | 🌉 Bridge 3.1 |
| Helly property (1-D) | 2 | [[Tutorial 1]] Q6 |
| Hypercube invariants | 5 | [[Tutorial 1]] Q1, [[Assignment 1]] Q2 |
| Induced P₃ exists | 1 | [[Tutorial 1]] Q3 |
| k-regular bipartite ⇒ perfect matching | 7 | [[Lec 03 — More on Hall's Theorem and Applications]] |
| k-regular girth 5 ⇒ n ≥ k²+1 | 3 | [[Tutorial 1]] Q2 |
| König's theorem | 7 | [[Lec 02 — König's Theorem and Hall's Theorem]] · [[2026-07-29 Matchings 2 — Berge and König]] |
| Königsberg impossible | 6 | [[2026-07-27 Euler Circuits]] |
| Latin rectangle extension | 7 | [[Lec 03 — More on Hall's Theorem and Applications]] |
| Leaf edge in some maximum matching | 7 | [[2026-07-29 Matchings 2 — Berge and König]] §2 |
| M ∪ N has Δ ≤ 2 | 7 | [[2026-07-29 Matchings 2 — Berge and König]] Claim 2.2 |
| MIS in a tree by dynamic programming | 4 | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] |
| Moon–Moser: ≤ 3^(n/3) maximal ind. sets | 4 | [[2026-07-29 Matchings 2 — Berge and König]] §2 |
| Lemma A: δ ≥ k ⇒ long path | 2 | [[2026-07-24 Preliminaries]] §6 |
| Lemma B: δ ≥ 2 ⇒ cycle | 2 | [[2026-07-24 Preliminaries]] §6 |
| Lemma C: δ ≥ k ⇒ cycle ≥ k+1 | 2 | [[2026-07-24 Preliminaries]] §6 |
| Long-path theorem | 2 | [[2026-07-24 Long Path Theorem]] |
| m > C(n−1,2) ⇒ connected | 3 | [[2026-07-24 Preliminaries]] §2 |
| Maximal vs longest | 2 | [[2026-07-24 Preliminaries]] §5 |
| MIS in trees (greedy on leaves) | 4 | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] |
| Min degree can't force k-connectivity | 8 | [[Assignment 1]] Q14 |
| Min-max duality family | 7 | 🌉 Bridge 7.1 |
| Moore bound | 3 | [[Assignment 1]] Q7 |
| ν ≤ τ | 7 | [[Lec 01 — Vertex Cover and Independent Set]] |
| ν ≤ τ ≤ 2ν (the sandwich, both tight) | 7 | [[2026-07-29 Matchings 2 — Berge and König]] §5 |
| ν ≤ ⌊n/2⌋ | 7 | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] |
| Odd cycle ⇒ not bipartite | 5 | [[2026-07-24 Preliminaries]] §9 |
| Path-or-cycle ≥ min{2δ, n} | 2 | [[Assignment 1]] Q9 |
| Q₄ is not planar | 9 | [[Tutorial 1]] Q1 |
| rad ≤ diam ≤ 2 rad | 1 | [[Assignment 1]] Q6 |
| SDR criterion | 7 | [[Lec 03 — More on Hall's Theorem and Applications]] |
| Shortest paths are induced | 1 | [[Tutorial 1]] Q5 |
| Subgraph vs induced vs spanning | 0 | 🌉 Bridge 0.1 |
| Tree: ≥ Δ(T) leaves | 4 | [[Assignment 1]] Q20 |
| Tree: L ≥ I + 2 (no degree 2) | 4 | [[Assignment 1]] Q21 |
| Tree: n−1 edges, unique paths | 4 | [[2026-07-24 Preliminaries]] §8 |
| Tree characterisations (Thm 1.5.1) | 4 | [[Assignment 1]] Q19 |
| Tree-order is a partial order | 4 | [[Assignment 1]] Q23 |
| Two longest paths meet | 2 | [[Tutorial 1]] Q4 |
| Universal vertex (bipartite, every max matching) | 7 | [[2026-08-10 Matchings in Bipartite Graphs]] §3 |
| Universal vertices ≥ \|MVC\| | 7 | [[2026-08-10 Matchings in Bipartite Graphs]] §4 |
| Walk contains a path | 1 | 🌉 Bridge 1.1 |
| δ ≥ 3 ⇒ even cycle | 2 | [[2026-07-24 Preliminaries]] §7 |
| κ ≤ λ ≤ δ, values for families | 8 | [[Assignment 1]] Q13 |

---

## If I only remember five things

1. **The extremal method** (Level 2) — take something maximal, ask what un-extendability forces. Nine results, one idea.
2. **Count two ways** (Level 3) — handshake and its descendants.
3. **Maximal ≠ maximum**, and maximal is nearly always enough — and *far* cheaper.
4. **Parity** decides more than it has any right to: bipartiteness, even cycles, Euler circuits, odd-degree counts.
5. **Min-max duality** (Bridge 7.1) — König, Hall, Menger, max-flow min-cut and Dilworth are one theorem in five costumes.

---

## Maintenance

This file is regenerated whenever new class notes are added. Every result should appear **exactly once** in a level and **once** in the index above, with a working link to the note holding the full proof.

