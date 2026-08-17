---
tags: [academics, graph-theory, nptel, lecture]
lecture: 1
unit: Covering Problems
source: NPTEL Graph Theory (Dr. L. Sunil Chandran, IISc) — Lecture 01
---

# Lec 01 — Introduction: Vertex Cover and Independent Set

**◀ Previous:** *(none — first lecture)* · **Index:** [[NPTEL Index]] · **Next ▶** [[Lec 02 — König's Theorem and Hall's Theorem]]

**Covered:** the four covering/packing parameters, how they pair up into complements, Gallai's two identities, the ν ≤ τ inequality, and why these problems are computationally hard.

> **Note on these notes.** These are my own worked-out write-ups of the mathematics — statements, proofs and examples reconstructed from scratch, not a transcript of the video. Where a proof can go several ways I give the cleanest standard route and flag alternatives.

---

## 0. Symbols used

| Symbol | Name | Meaning |
|---|---|---|
| **α(G)** | independence number | size of the **largest independent set** |
| **τ(G)** | vertex cover number | size of the **smallest vertex cover** |
| **ν(G)** | matching number | size of the **largest matching** |
| **ρ(G)** | edge cover number | size of the **smallest edge cover** |
| **ω(G)** | clique number | size of the largest clique |
| **Ḡ** | complement | same vertices; edges exactly where G has none |
| **n** | order | number of vertices |

> Mnemonic for the Greek letters: **α** and **ν** are the two things you **maximise** (independent set, matching). **τ** and **ρ** are the two you **minimise** (vertex cover, edge cover).

---

## 1. The four definitions

### Independent set

> A set **S ⊆ V** is **independent** if **no edge has both endpoints in S**.

Think: a set of mutually non-adjacent vertices — no two of them "see" each other.

```
   a ——— b        {a, c} is independent  ✓  (no edge a–c)
   |     |        {a, b} is NOT           ✗  (edge a–b exists)
   d ——— c
```

### Vertex cover

> A set **K ⊆ V** is a **vertex cover** if **every edge has at least one endpoint in K**.

Think: put guards on vertices so that every edge is watched from at least one end.

```
   a ——— b        K = {a, c} covers every edge:
   |     |        ab ✓(a)  bc ✓(c)  cd ✓(c)  da ✓(a)
   d ——— c
```

### Matching

> A set **M ⊆ E** is a **matching** if **no two edges of M share a vertex**.

Think: pair people up; nobody is in two pairs.

### Edge cover

> A set **F ⊆ E** is an **edge cover** if **every vertex is an endpoint of some edge in F**.

Think: every vertex must be touched by at least one chosen edge.

> ⚠️ **An edge cover only exists if G has no isolated vertex** — a vertex with no edges can never be covered. Assume this throughout when ρ appears.

### The pattern

Notice the pleasing symmetry — these are the same idea with vertices and edges swapped:

| | **packing** (max, disjointness) | **covering** (min, hit everything) |
|---|---|---|
| **vertices** | independent set **α** | vertex cover **τ** |
| **edges** | matching **ν** | edge cover **ρ** |

---

## 2. ★ Independent sets and vertex covers are complements

> **Theorem.** S is an independent set **⟺** V ∖ S is a vertex cover.

**Proof.** Chase the definitions — both sides say the same thing about edges.

$$S \text{ independent} \iff \text{no edge has \textbf{both} ends in } S \iff \text{every edge has \textbf{at least one} end outside } S$$

and "every edge has at least one end in V ∖ S" is precisely the definition of V ∖ S being a vertex cover ✓ ∎

### Gallai's first identity

> **Corollary.** $\alpha(G) + \tau(G) = n$

**Proof.** Take a **maximum** independent set S, so |S| = α. Then V ∖ S is a vertex cover of size n − α, so τ ≤ n − α, i.e.

$$\alpha + \tau \le n.$$

Now take a **minimum** vertex cover K, so |K| = τ. Then V ∖ K is independent of size n − τ, so α ≥ n − τ, i.e.

$$\alpha + \tau \ge n.$$

Both directions together give equality ✓ ∎

**Check on the 4-cycle.** C₄ = a–b–c–d–a: α = 2 ({a,c}), τ = 2 ({a,c}), n = 4 ✓
**Check on K₅:** α = 1 (any two vertices are adjacent), τ = 4, n = 5 ✓

> **Why this matters:** the two problems are the *same problem wearing different clothes*. Solve one and you've solved the other. In particular, if one is computationally hard then so is the other — see §5.

### And a third disguise: cliques

> S is independent in G **⟺** S is a **clique** in the complement Ḡ.

*Why:* independent in G means no edges inside S; in Ḡ every non-edge of G becomes an edge, so S becomes all-adjacent ✓

$$\alpha(G) = \omega(\bar G)$$

So **independent set, vertex cover and clique are three views of one problem.**

---

## 3. ★ ν(G) ≤ τ(G) — matchings bound covers from below

> **Theorem.** For every graph, $\nu(G) \le \tau(G)$.

**Proof.** Let M be a maximum matching, |M| = ν, and let K be any vertex cover.

K must cover **every** edge, in particular every edge of M. So for each of the ν edges in M, K contains at least one of its two endpoints.

The edges of M are **pairwise disjoint** — that's what makes M a matching — so these chosen endpoints are **ν distinct vertices**, all in K. Hence |K| ≥ ν.

This holds for every vertex cover, so it holds for the smallest: **τ ≥ ν** ✓ ∎

```
 M = three disjoint edges          any cover needs ≥ 1 vertex per edge,
 ●━━●    ●━━●    ●━━●              and the edges share nothing
                                    →  at least 3 vertices
```

### When is it equality? When is it strict?

- **Triangle K₃:** ν = 1 (any two edges share a vertex), τ = 2 (one vertex misses the opposite edge). So **1 < 2 — strict** ✗
- **Any bipartite graph:** equality always. That's **König's theorem** — the subject of [[Lec 02 — König's Theorem and Hall's Theorem]].

> **The odd cycle is the obstruction.** K₃ is the smallest example where ν < τ, and bipartite graphs are exactly the graphs with no odd cycle (see [[2026-07-24 Preliminaries]] §9). That's not a coincidence — it's the whole reason König's theorem needs bipartiteness.

---

## 4. ★ Gallai's second identity: ν(G) + ρ(G) = n

> **Theorem.** If G has **no isolated vertices**, then $\nu(G) + \rho(G) = n$.

This is the edge-side twin of α + τ = n. The proof is prettier because the two directions are built by different constructions.

### Direction 1: ρ ≤ n − ν

Take a **maximum matching** M, with ν edges. It covers exactly **2ν** vertices, leaving **n − 2ν** vertices untouched.

Since there are no isolated vertices, each untouched vertex u has *some* edge; pick one such edge per untouched vertex and add it in.

```
 matched pairs:  ●━━●  ●━━●          2ν vertices covered by ν edges
 leftovers:      ●  ●  ●             each grabs one edge of its own
                 └┐ └┐ └┐
```

The result covers every vertex, so it's an edge cover, using

$$\nu + (n - 2\nu) = n - \nu \quad\text{edges} \quad\Longrightarrow\quad \rho \le n - \nu. \;✓$$

### Direction 2: ν ≥ n − ρ

Take a **minimum edge cover** F, with ρ edges. Look at F as a subgraph.

**Claim: every component of F is a star** (one centre joined to some leaves).

*Why:* if some component contained a path on four vertices u–v–w–x, then the middle edge **vw is redundant** — u and v are still covered by uv, and w and x by wx. Dropping it would give a smaller edge cover ✗ Similarly no component contains a cycle (drop any cycle edge — its endpoints are still covered by the neighbouring cycle edges) ✗ So each component is a tree with no path on four vertices, which is exactly a **star**.

Now count. Let the components be stars with k₁, …, k_c edges. A star with kᵢ edges has kᵢ + 1 vertices, and every vertex of G is in exactly one component (F covers everything), so

$$\sum_i (k_i + 1) = n, \qquad \sum_i k_i = \rho \quad\Longrightarrow\quad c = n - \rho.$$

Pick **one edge from each star**. Different stars are vertex-disjoint, so these c edges form a **matching**:

$$\nu \ge c = n - \rho. \;✓$$

### Combine

ρ ≤ n − ν gives ν + ρ ≤ n; ν ≥ n − ρ gives ν + ρ ≥ n. Hence

$$\nu(G) + \rho(G) = n. \qquad \blacksquare$$

**Check on the path a–b–c (n = 3).** ν = 1 (edges ab and bc share b), ρ = 2 (need both edges to touch a and c). 1 + 2 = 3 ✓
**Check on C₄ (n = 4).** ν = 2, ρ = 2. 2 + 2 = 4 ✓
**Check on K₄ (n = 4).** ν = 2 (a perfect matching), ρ = 2. Sum 4 ✓

> **Both identities in one line:** α + τ = n pairs *maximum independent set* with *minimum vertex cover*; ν + ρ = n pairs *maximum matching* with *minimum edge cover*. In each case, solving the max problem hands you the min problem for free.

---

## 5. Why these problems are hard

**Vertex Cover** is one of Karp's original 21 NP-complete problems (1972). By the complement identity of §2, so are **Independent Set** and **Clique** — an efficient algorithm for any one of them would solve all three.

**The contrast worth remembering:**

| Problem | General graphs | Bipartite graphs |
|---|---|---|
| Maximum **matching** ν | **polynomial** (Edmonds' blossom algorithm) | polynomial (Hopcroft–Karp) |
| Minimum **vertex cover** τ | **NP-hard** | **polynomial** — via König, τ = ν |
| Maximum **independent set** α | **NP-hard** | polynomial — via α = n − τ |

So bipartiteness collapses a hard problem into an easy one, entirely because König's theorem forces ν = τ there. That single equality is why the next lecture matters so much.

---

## 6. Summary of relationships

$$\alpha + \tau = n \qquad \nu + \rho = n \ \ (\text{no isolated vertices}) \qquad \nu \le \tau$$

and combining the first with the third:

$$\nu \;\le\; \tau \;=\; n - \alpha.$$

**All four on C₄** (n = 4): α = 2, τ = 2, ν = 2, ρ = 2 — everything equal, since C₄ is bipartite.
**All four on K₃** (n = 3): α = 1, τ = 2, ν = 1, ρ = 2. Check: 1+2 = 3 ✓, 1+2 = 3 ✓, and ν = 1 < 2 = τ ✓ (K₃ is not bipartite).

---

## Takeaways

1. **Independent set and vertex cover are complements** — one set, two names. Everything else follows from that.
2. **Cliques are the same problem again**, viewed in the complement graph.
3. **ν ≤ τ always**, because a matching's edges are disjoint and each demands its own cover vertex.
4. **Odd cycles are what break equality** — K₃ is the minimal witness of ν < τ.
5. **Gallai's identities** both say: *the maximum packing and the minimum covering add to n.* The proofs are constructions — extend a maximum matching to an edge cover; pick one edge per star.
6. **Minimum edge covers decompose into stars.** Any longer path would contain a droppable middle edge.
7. **Bipartiteness turns NP-hard into polynomial** — via König.

---

## Doubts / to revisit

- [ ] Confirm the lecture's exact route for Gallai's ν + ρ = n; I used the maximum-matching-extension proof, which is standard. Some courses derive it from König instead.
- [ ] Edmonds' blossom algorithm is mentioned here but not proved — comes later in the matchings unit.
