---
tags: [academics, graph-theory, assignment]
type: assignment
source: Diestel, Graph Theory — Chapter 1 exercises
date: 2026-07-29
---

# Assignment 1 — Diestel Ch. 1 (23 problems)

**Hub:** [[Graph Theory]] · **Background notes:** [[2026-07-24 Preliminaries]] · [[2026-07-24 Long Path Theorem]] · [[2026-07-27 Euler Circuits]]

> Diestel marks exercises: **−** = easier, **+** = harder, no mark = standard.

> **Note on the source text.** A few problems refer to numbered results (Prop 1.3.2, Thm 1.3.4, Thm 1.4.3, Thm 1.5.1). Numbering shifts between editions, so I state each result before using it — check it matches your copy. Where a problem genuinely needs the book's *proof* in front of you (Q17, and the exact constant in Q18), I say so rather than guess.

> **Symbols reconstructed from the paste.** Some `≤`/`≥` signs were lost when you copied. I read Q6 as `rad(G) ≤ diam(G) ≤ 2·rad(G)`, Q7 as `|G| ≥ n₀(d/2, g)`, Q8 as `δ(G) ≤ f(n)`, Q9 as `≥ min{2δ(G), |G|}`.

---

## Recurring toolkit

Almost every problem here uses one of four moves. Worth naming them up front:

| Move | What it says |
|---|---|
| **Handshake** | Σ deg(v) = 2m — count edge-endpoints two ways |
| **Extremal object** | take a *longest path* / *minimal subgraph*; extremality forces structure |
| **Distance layers** | group vertices by d(v₀, ·); adjacent vertices sit in the same or neighbouring layer |
| **Ball counting** | if girth is large, balls around a vertex are trees, so they grow like (d−1)ⁱ |

---

# Q1 − Number of edges in Kⁿ

**Answer.** $\binom{n}{2} = \dfrac{n(n-1)}{2}$

**Why.** In Kⁿ every pair of distinct vertices is joined by exactly one edge. So edges correspond one-to-one with **2-element subsets** of the vertex set, and there are C(n,2) of those.

**Cross-check via handshake.** Every vertex is adjacent to the other n−1, so deg(v) = n−1 for all v:

$$2m = \sum_v \deg(v) = n(n-1) \quad\Longrightarrow\quad m = \frac{n(n-1)}{2} \;✓$$

**Numbers.** K₃: 3·2/2 = 3 (triangle ✓). K₄: 4·3/2 = 6 ✓. K₅: 10 ✓

---

# Q2 The d-dimensional cube $Q_d$

**Setup.** V = {0,1}ᵈ — all 0–1 strings of length d. Two strings are adjacent iff they differ in **exactly one** position.

```
 Q1: 0——1        Q2:  00——01        Q3: a cube, 8 corners
                       |    |
                      10——11
```

### Number of vertices

Each of the d positions is 0 or 1 independently → **|V| = 2ᵈ**.

### Degree of every vertex, and average degree

From a string x you reach exactly one neighbour per position (flip that bit), and different positions give different neighbours. So **every vertex has degree exactly d** — the cube is **d-regular**.

$$\text{average degree } = d$$

### Number of edges

Handshake:

$$2m = \sum_v \deg(v) = 2^d \cdot d \quad\Longrightarrow\quad \boxed{m = d\,2^{\,d-1}}$$

**Check.** Q₃: 3·2² = 12 edges — a cube has 12 edges ✓

### Diameter

**Key fact:** d(x,y) = **Hamming distance** H(x,y) = number of positions where x and y differ.

- *≥*: each edge changes exactly **one** bit, so getting from x to y needs at least H(x,y) steps.
- *≤*: fix the differing positions one at a time — H(x,y) steps, each a legal edge.

Maximum Hamming distance is d (from 00…0 to 11…1), so

$$\operatorname{diam}(Q_d) = d$$

### Girth

- $Q_d$ is **bipartite**: split by the parity of the number of 1s. Flipping one bit always flips the parity, so every edge crosses the two sides → **no odd cycles**.
- A 4-cycle exists as soon as d ≥ 2: `00…0 → 10…0 → 110…0 → 010…0 → 00…0`.

$$g(Q_d) = 4 \quad (d \ge 2), \qquad g(Q_1) = \infty \ \text{(no cycle at all)}$$

### Circumference

**Claim: $Q_d$ has a Hamiltonian cycle for d ≥ 2, so the circumference is 2ᵈ.**

*(A cycle can't be longer than the number of vertices, so 2ᵈ is also the ceiling — this is exactly optimal.)*

**Proof by induction on d** (the hint).

- **Base d = 2.** Q₂ is the 4-cycle `00 – 01 – 11 – 10 – 00` ✓
- **Step.** Assume $Q_d$ has a Hamiltonian cycle. Delete one edge of it to get a **Hamiltonian path** P from a to b covering all of $Q_d$.

  Now $Q_{d+1}$ splits into two copies of $Q_d$: strings starting **0** and strings starting **1**, with each 0x joined to its twin 1x.

  ```
  0-copy:   0a ──── P ────▶ 0b
                             │   (edge 0b–1b, twins)
  1-copy:   1a ◀─── P ───── 1b
             │
             └──── edge 1a–0a, twins ────┘
  ```

  Traverse `0a →P→ 0b`, cross the twin edge to `1b`, traverse P **backwards** to `1a`, then cross the twin edge back to `0a`. Every vertex of both copies is used exactly once → a Hamiltonian cycle of $Q_{d+1}$ ✓

$$\text{circumference}(Q_d) = 2^d \quad (d \ge 2)$$

### Summary table

| Invariant | Value |
|---|---|
| vertices | 2ᵈ |
| average degree | d (it's d-regular) |
| edges | d·2ᵈ⁻¹ |
| diameter | d |
| girth | 4 (for d ≥ 2) |
| circumference | 2ᵈ (Hamiltonian, d ≥ 2) |

---

# Q3 Long path between two cycle vertices ⇒ long cycle

**Statement.** G contains a cycle C, and a path P of length ≥ k between two vertices of C. Show G contains a cycle of length ≥ √k.

**The idea.** P starts and ends on C, but in between it may wander on and off C. Mark the points where it touches C. Then either **one detour is long** (long detour + arc of C = big cycle), or **there are many touch points** (so C itself is big). One of the two must happen — that's the whole proof.

**Proof.** Let P's vertices that lie on C be, in the order they occur along P,

$$p_0,\; p_1,\; \dots,\; p_{s-1} \qquad (s \ge 2,\ \text{since both endpoints of } P \text{ are on } C).$$

These cut P into **s − 1 segments** S₁,…,S₍ₛ₋₁₎, where Sⱼ runs from pⱼ₋₁ to pⱼ and touches C **only at its two endpoints**. Their lengths sum to the length of P:

$$\ell_1 + \ell_2 + \cdots + \ell_{s-1} \;=\; |P| \;\ge\; k.$$

**Case 1 — some segment is long: ℓⱼ ≥ √k.**

Sⱼ joins two *distinct* vertices a = pⱼ₋₁ and b = pⱼ of C (distinct because P is a path and never repeats a vertex), and its interior avoids C. Those two points split C into two arcs; pick either arc A. Then **Sⱼ ∪ A is a cycle**, of length

$$\ell_j + |A| \;\ge\; \ell_j \;\ge\; \sqrt{k}\;✓$$

**Case 2 — every segment is short: ℓⱼ < √k for all j.**

Then

$$k \;\le\; \sum_{j} \ell_j \;<\; (s-1)\sqrt{k} \quad\Longrightarrow\quad s-1 > \frac{k}{\sqrt k} = \sqrt k .$$

So P touches C in s > √k + 1 distinct vertices. But all of those lie **on C**, so C has more than √k vertices, i.e.

$$|C| \;>\; \sqrt k \;✓$$

and **C itself** is the cycle we wanted. ∎

> **What makes it work:** total length k has to go *somewhere*. Either it piles into one segment (Case 1) or it spreads across many segments (Case 2) — and √k is exactly the balance point where both branches give the same guarantee.

---

# Q4 − Is the bound in Proposition 1.3.2 best possible?

**The proposition** *(check against your edition)*:

> Every graph G containing a cycle satisfies **g(G) ≤ 2·diam(G) + 1**, where g = girth.

**Answer: yes, best possible** — the bound is attained with equality, so it cannot be lowered.

**Witness: odd cycles.** Take G = C²ᵏ⁺¹ (a cycle on 2k+1 vertices).

- **girth** = 2k+1 (the whole cycle is the only cycle)
- **diameter** = ⌊(2k+1)/2⌋ = k (walk the shorter way round)

$$2\operatorname{diam}(G) + 1 = 2k + 1 = g(G) \quad\text{— equality} \;✓$$

**Numbers.** C₅: girth 5, diameter 2, bound 2·2+1 = 5 ✓ exactly tight.
The Petersen graph also achieves it: girth 5, diameter 2 ✓

**Not always tight:** even cycles C²ᵏ have girth 2k and diameter k, so the bound gives 2k+1 > 2k — true but slack. "Best possible" only requires that *some* graph attains it.

---

# Q5 Distance layers

**Setup.** v₀ ∈ G, D₀ := {v₀}, and for n ≥ 1

$$D_n := N_G(D_0 \cup \cdots \cup D_{n-1}).$$

Recall Diestel's convention: for a set U, **N(U) is the set of vertices *outside* U that have a neighbour in U.**

### Part (a): Dₙ = { v : d(v₀,v) = n }

**Proof by induction on n.**

- **n = 0.** D₀ = {v₀} and d(v₀,v₀) = 0 ✓
- **Step.** Suppose Dᵢ = {v : d(v₀,v) = i} for every i ≤ n−1. Then

$$D_0 \cup \cdots \cup D_{n-1} = \{\, v : d(v_0,v) \le n-1 \,\} \;=:\; B.$$

  **(⊆)** Let v ∈ Dₙ = N(B). Then v ∉ B, so **d(v₀,v) ≥ n**. Also v has a neighbour u ∈ B, so d(v₀,u) ≤ n−1 and therefore

$$d(v_0,v) \le d(v_0,u) + 1 \le n.$$

  Both together force **d(v₀,v) = n** ✓

  **(⊇)** Let d(v₀,v) = n. Then v ∉ B. Take a shortest v₀–v path and let u be the vertex just before v; then d(v₀,u) = n−1, so u ∈ B and v is adjacent to u. Hence v ∈ N(B) = Dₙ ✓

### Part (b): Dₙ₊₁ ⊆ N(Dₙ) ⊆ Dₙ₋₁ ∪ Dₙ₊₁

**Tiny lemma used twice.** If u ~ v then **|d(v₀,u) − d(v₀,v)| ≤ 1**.
*Why:* walk to u then take the edge → d(v₀,v) ≤ d(v₀,u)+1; and symmetrically.

**Dₙ₊₁ ⊆ N(Dₙ).** Let v ∈ Dₙ₊₁, so d(v₀,v) = n+1. On a shortest v₀–v path, the vertex u just before v has d(v₀,u) = n, i.e. u ∈ Dₙ. And v ∉ Dₙ (its distance is n+1 ≠ n). So v is a neighbour of Dₙ lying outside it → v ∈ N(Dₙ) ✓

**N(Dₙ) ⊆ Dₙ₋₁ ∪ Dₙ₊₁.** Let v ∈ N(Dₙ): then v ∉ Dₙ and v ~ u for some u with d(v₀,u) = n. By the lemma d(v₀,v) ∈ {n−1, n, n+1}. Since v ∉ Dₙ we can drop n. So d(v₀,v) ∈ {n−1, n+1}, i.e. **v ∈ Dₙ₋₁ ∪ Dₙ₊₁** ✓ ∎

> **Picture.** Layers stack like onion rings around v₀. An edge never jumps a ring — it either stays inside one ring or steps to an adjacent one.
> ```
>        D₀   D₁   D₂   D₃
>        v₀ — ●  — ●  — ●        edges go ↔ neighbouring layers,
>              ●    ●             or within a layer — never further
> ```

---

# Q6 rad(G) ≤ diam(G) ≤ 2·rad(G)

**Definitions.** For a **connected** G:

- **eccentricity** ecc(v) = max over u of d(v,u) — how far the furthest vertex is from v
- **radius** rad(G) = min over v of ecc(v) — the best possible "central" position
- **diameter** diam(G) = max over u,v of d(u,v) = max over v of ecc(v)

### Left inequality: rad ≤ diam

rad is a **minimum** of the ecc values and diam is their **maximum**. A minimum never exceeds a maximum ✓

### Right inequality: diam ≤ 2·rad

Let **z** be a *centre* — a vertex achieving ecc(z) = rad(G). For **any** two vertices u, v, route through z and use the triangle inequality:

$$d(u,v) \;\le\; d(u,z) + d(z,v) \;\le\; \operatorname{rad}(G) + \operatorname{rad}(G) = 2\operatorname{rad}(G),$$

since z is within rad(G) of *everything*. Taking the maximum over u,v gives **diam ≤ 2·rad** ✓ ∎

**Both are tight.**

- **Left:** any cycle Cⁿ has rad = diam = ⌊n/2⌋ ✓
- **Right:** the path on 3 vertices `a — b — c` has rad = 1 (centre b) and diam = 2 = 2·1 ✓

> **Intuition:** the centre is at most rad from everyone, so nobody is more than "two radii" from anyone else — exactly the reasoning that a circle of radius r has diameter 2r.

---

# Q7 Moore bound with minimum degree

**Theorem 1.3.4** (the version with **average** degree): if d(G) ≥ d and g(G) ≥ g then |G| ≥ n₀(d,g), where

$$n_0(d,g) := \begin{cases} 1 + d\sum_{i=0}^{r-1}(d-1)^i & g = 2r+1 \ \text{(odd)}\\[4pt] 2\sum_{i=0}^{r-1}(d-1)^i & g = 2r \ \ \ \ \text{(even)}\end{cases}$$

### Part (a): prove the weakening — δ(G) ≥ d and g(G) ≥ g ⇒ |G| ≥ n₀(d,g)

**The idea.** Grow a ball outward from a vertex. Large girth means the ball has **no shortcuts** — it's a tree — so each level multiplies by (d−1). Count the levels.

**Key structural fact.** If g ≥ 2r+1 then for every i ≤ r, each vertex at distance i from v has **exactly one** neighbour at distance i−1.

*Why:* suppose w at distance i had two neighbours u₁ ≠ u₂ at distance i−1. Take shortest paths from v to u₁ and to u₂ and let z be their **last common vertex**. Then

$$z \to u_1 \to w \to u_2 \to z$$

is a cycle of length ≤ (i−1−d(v,z)) + 1 + 1 + (i−1−d(v,z)) = 2i − 2d(v,z) ≤ 2i ≤ 2r < g. That contradicts girth ≥ g ✓

**Odd case, g = 2r+1.** Pick any vertex v and count by distance:

| level | count |
|---|---|
| 0 | 1 |
| 1 | ≥ d |
| i (2 ≤ i ≤ r) | ≥ d(d−1)ⁱ⁻¹ |

Level i grows by ≥ (d−1) per vertex: each vertex at level i−1 has ≥ d neighbours, exactly one pointing back inward, leaving ≥ d−1 pointing outward — and by the structural fact no two of them coincide. Summing:

$$|G| \;\ge\; 1 + \sum_{i=1}^{r} d(d-1)^{i-1} \;=\; 1 + d\sum_{i=0}^{r-1}(d-1)^i \;=\; n_0(d,2r+1)\;✓$$

**Even case, g = 2r.** Start from an **edge** xy instead of a vertex, and count vertices within distance r−1 of x or of y.

- The two sets are **disjoint**: a vertex within r−1 of both would close a cycle of length ≤ (r−1)+(r−1)+1 = 2r−1 < g.
- From x, avoiding the y-side, level i has ≥ (d−1)ⁱ vertices for 0 ≤ i ≤ r−1.

$$|G| \;\ge\; 2\sum_{i=0}^{r-1}(d-1)^i \;=\; n_0(d,2r)\;✓ \qquad \blacksquare$$

### Part (b): deduce |G| ≥ n₀(d/2, g) for the average-degree version

Suppose only that **d(G) ≥ d** (average degree). Recall ε(G) = m/n = d(G)/2 ≥ d/2, and from [[2026-07-24 Preliminaries]] §4:

> every graph with an edge has a subgraph H with δ(H) ≥ ε(G).

So there is H ⊆ G with **δ(H) ≥ d/2**. Also **g(H) ≥ g(G) ≥ g** — deleting vertices and edges can only destroy cycles, never create shorter ones. Apply part (a) to H:

$$|G| \;\ge\; |H| \;\ge\; n_0(d/2,\; g)\;✓ \qquad \blacksquare$$

> **The moral:** average degree is too weak to count with directly, so you first *upgrade* it to a minimum-degree statement on a subgraph — at the cost of halving it. That halving is exactly why the conclusion has d/2 rather than d.

---

# Q8 Girth ≥ 5 forces δ(G) = o(n)

**Goal.** Find f with f(n)/n → 0 and δ(G) ≤ f(n) for every graph of girth ≥ 5 and order n.

**We'll prove the sharp form: δ(G) ≤ √(n−1).** Then f(n) = √n does the job, since √n / n = 1/√n → 0 ✓

**What girth ≥ 5 buys us.** No cycle of length 3 or 4, which means:

1. **No triangle** → N(v) is an independent set (no edges inside a neighbourhood).
2. **No 4-cycle** → any two vertices have **at most one** common neighbour.

**Proof.** Let δ = δ(G) and pick any vertex v. Write N = N(v), so |N| ≥ δ. Now count vertices in three disjoint groups.

- **{v}** — 1 vertex.
- **N** — at least δ vertices.
- For each u ∈ N, the set **N(u) ∖ ({v} ∪ N)** — the neighbours of u further out.

Three things to check, and each is exactly one of the girth conditions:

- *Each such set has ≥ δ−1 vertices.* u has ≥ δ neighbours; one is v; and **none of the others lies in N**, because u ~ u′ with u, u′ ∈ N would make the triangle v–u–u′–v ✗
- *These sets are pairwise disjoint.* If u₁ ≠ u₂ in N shared an outer neighbour w, then v–u₁–w–u₂–v is a **4-cycle** ✗
- *They avoid {v} ∪ N by construction* ✓

Adding up:

$$n \;\ge\; 1 + |N| + \sum_{u \in N}\big|N(u)\setminus(\{v\}\cup N)\big| \;\ge\; 1 + \delta + \delta(\delta-1) \;=\; 1 + \delta^2 .$$

Hence **δ² ≤ n − 1**, that is

$$\delta(G) \;\le\; \sqrt{n-1}. \qquad \blacksquare$$

Taking f(n) = √n: f(n)/n = 1/√n → 0 and δ(G) ≤ √(n−1) ≤ f(n) ✓

**Sanity check.** The Petersen graph has girth 5, n = 10, δ = 3. Bound: √9 = 3 ✓ **exactly tight.**

> **Reading it in reverse:** to have every vertex of degree ≥ δ *without* short cycles, you need roughly δ² vertices — a vertex, its δ neighbours, and δ(δ−1) more beyond, all forced to be distinct. Sparse local structure demands global room.

---

# Q9 + Path *or cycle* of length ≥ min{2δ(G), |G|}

**Compare with what we already proved.** In [[2026-07-24 Long Path Theorem]] we showed a connected G has a **path** of length ≥ min{2δ, n−1}. This asks for more: length ≥ min{2δ, **n**}. Since a path on n vertices has length only n−1, reaching **n** is impossible for a path — so when the bound bites, the answer must be a **cycle**. That's why the statement says "path *or* cycle".

**Proof.** Let P = v₀ v₁ … vₖ be a **longest path** in G, of length k. As established in the companion note, both endpoints are trapped: every neighbour of v₀ and of vₖ lies on P.

**Case 1: k ≥ 2δ.** Then P itself is a path of length ≥ 2δ ≥ min{2δ, n} ✓ Done.

**Case 2: k ≤ 2δ − 1.** Run the pigeonhole argument from the companion note. Put

$$A = \{\, i : v_0 \sim v_i \,\}, \qquad B = \{\, i : v_k \sim v_{i-1} \,\},$$

both inside {1,…,k}, both of size ≥ δ. Since |A| + |B| ≥ 2δ > k, they **overlap** at some index i, giving the two crossing edges v₀ ~ vᵢ and vₖ ~ vᵢ₋₁. Fold P into a cycle:

$$C:\quad v_0 \to v_1 \to \cdots \to v_{i-1} \to v_k \to v_{k-1} \to \cdots \to v_i \to v_0$$

covering **all k+1 vertices of P**.

**Now the new step: C must contain every vertex of G.**
Suppose some vertex w lies off C. Since G is connected, some vertex vⱼ of C has an edge to a vertex outside C. Snip a cycle-edge at vⱼ to reopen C into a path on all k+1 vertices ending at vⱼ, then attach that outside vertex → a path of length k+1, **longer than P**. Contradiction ✗

So C spans all n vertices, i.e. C is a **Hamiltonian cycle** of length exactly **n**:

$$\text{length}(C) = n \;\ge\; \min\{2\delta,\, n\}\;✓ \qquad \blacksquare$$

> **The upgrade in one line:** the earlier proof *discarded* the cycle after using it for a contradiction. Here we notice that the very same contradiction proves the cycle is **spanning** — so instead of throwing it away, we hand it back as the answer.

**Check.** Kⁿ: δ = n−1, so min{2n−2, n} = n for n ≥ 2, and Kⁿ does have a Hamiltonian cycle ✓ Cⁿ: δ = 2, min{4, n} = 4 for n ≥ 4, and Cⁿ has a cycle of length n ≥ 4 ✓

---

# Q10 Diameter k and minimum degree d ⇒ about kd/3 vertices

### Part (a): the lower bound

**The idea.** Walk along a longest shortest-path and grab every **third** vertex. Those vertices are so far apart that their neighbourhoods can't overlap — so the neighbourhoods tile up to give a vertex count.

**Proof.** Pick u, v with d(u,v) = k = diam(G), and a shortest path

$$u = x_0,\ x_1,\ \dots,\ x_k = v.$$

Consider the vertices **x₀, x₃, x₆, …** — every third one. There are ⌊k/3⌋ + 1 of them.

**Claim: their closed neighbourhoods N[x₃ᵢ] are pairwise disjoint.**
On a shortest path, d(x₃ᵢ, x₃ⱼ) = 3|i − j| ≥ 3 for i ≠ j. If some vertex w lay in both N[x₃ᵢ] and N[x₃ⱼ], then

$$d(x_{3i}, x_{3j}) \le d(x_{3i}, w) + d(w, x_{3j}) \le 1 + 1 = 2 < 3 \quad ✗$$

Each closed neighbourhood has |N[x]| ≥ d + 1 (the vertex plus its ≥ d neighbours). Disjointness lets us just add:

$$n \;\ge\; \Big(\Big\lfloor \tfrac{k}{3} \Big\rfloor + 1\Big)(d+1) \;\approx\; \frac{kd}{3}. \qquad \blacksquare$$

### Part (b): and not substantially more

We build a graph with diameter k, minimum degree ≥ d, and only about kd/3 vertices — showing the bound is the right order.

**Construction — a "thickened path".** Take layers L₀, L₁, …, Lₖ where:

- each layer is a **clique**,
- **consecutive** layers are joined completely,
- non-consecutive layers have no edges,
- |Lᵢ| = s := ⌈(d+1)/3⌉ for the interior layers, and |L₀| = |Lₖ| = d+1 for the two ends.

```
 L₀ ═══ L₁ ═══ L₂ ═══ ... ═══ L_k
 (each Lᵢ a clique; ═ means "join every vertex to every vertex")
```

- **Distances:** d(Lᵢ, Lⱼ) = |i − j|, so **diam = k** ✓
- **Degrees:** an interior vertex sees its own layer plus both neighbours: (s−1) + s + s = 3s − 1 ≥ d ✓; the end layers are cliques of size d+1, so those vertices have degree ≥ d ✓
- **Order:** (k−1)s + 2(d+1) ≈ **kd/3 + O(d)** ✓

So kd/3 is correct up to a constant factor and an additive O(d) — you cannot force substantially more vertices. ∎

> **Why *every third*?** Two vertices at distance 2 can share a neighbour, so neighbourhoods at spacing 2 may overlap. Distance 3 is the first gap that guarantees disjointness — and that "3" is exactly the 3 in kd/3.

---

# Q11 − Components partition the vertex set

**Goal.** Every vertex lies in **exactly one** component (= maximal connected subgraph).

**Proof via an equivalence relation.** Define on V(G):

$$u \sim v \quad :\Longleftrightarrow \quad G \text{ contains a } u\text{–}v \text{ path}.$$

**It's an equivalence relation:**

- **Reflexive.** The single-vertex path from u to u ✓
- **Symmetric.** Reverse the path ✓
- **Transitive.** A u–v path followed by a v–w path is a u–w **walk**; and every walk from u to w contains a u–w **path** (repeatedly cut out the loop between two visits to a repeated vertex — each cut shortens the walk, so the process ends) ✓

Equivalence relations **partition** their ground set — that's the standard fact — so the classes are non-empty, pairwise disjoint, and cover V.

**The classes are exactly the components.**

- Each class induces a **connected** subgraph: any two of its vertices are joined by a path, and every vertex of that path is again in the class (it's joined to both ends).
- Each class is **maximal**: a vertex outside the class has no path to any vertex inside it, so adding it cannot keep the subgraph connected.

Hence components = equivalence classes, and since the classes partition V, **every vertex lies in exactly one component** ✓ ∎

---

# Q12 − Every 2-connected graph contains a cycle

**Definition.** G is **2-connected** if |G| > 2 and G − v is connected for every single vertex v.

**Proof.** We show **δ(G) ≥ 2**, then quote a lemma we already proved.

Suppose some vertex v had degree ≤ 1.

- **deg(v) = 0.** Then G itself is disconnected (|G| ≥ 3 means there's something else), contradicting 2-connectedness ✗
- **deg(v) = 1**, with sole neighbour u. Remove u. Then v has no edges left, and G − u still has ≥ 2 vertices, so **G − u is disconnected** ✗

Either way we contradict 2-connectedness. So **δ(G) ≥ 2**, and by **Lemma B** of [[2026-07-24 Preliminaries]] §6:

> δ(G) ≥ 2 ⇒ G contains a cycle ✓ ∎

**Alternative one-liner.** If G were acyclic and connected it would be a **tree** on ≥ 3 vertices, which has an internal (non-leaf) vertex v; deleting v disconnects the tree — contradicting 2-connectedness.

---

# Q13 Connectivity of the standard families

**Notation.** $P^m$ = path of **length** m (so m+1 vertices), $C^n$ = cycle on n vertices, $K^n$ = complete graph, $K^{m,n}$ = complete bipartite with parts of size m and n, $Q_d$ = the d-cube. Throughout d, m, n ≥ 3.

**Always useful:** $\kappa(G) \le \lambda(G) \le \delta(G)$ — vertex-connectivity ≤ edge-connectivity ≤ minimum degree.

| G | κ (vertex) | λ (edge) | reason |
|---|---|---|---|
| $P^m$ | 1 | 1 | delete any interior vertex, or any edge, and it falls apart |
| $C^n$ | 2 | 2 | one deletion leaves a path (still connected); two suffice to break it |
| $K^n$ | n−1 | n−1 | you can never disconnect Kⁿ — by convention κ = n−1; also δ = n−1 |
| $K^{m,n}$ | min(m,n) | min(m,n) | delete the smaller side entirely |
| $Q_d$ | d | d | d-regular and d-connected |

**Working through the less obvious ones.**

**$K^{m,n}$**, parts A (size m) and B (size n), say m ≤ n.
- *κ ≤ m*: delete all of A; B is an independent set with n ≥ 2 vertices left, hence disconnected ✓
- *κ ≥ m*: any two vertices are joined by m internally disjoint paths, so fewer than m deletions can't separate them. Hence **κ = min(m,n)**.
- *λ*: degrees are n (for A-vertices) and m (for B-vertices), so δ = min(m,n) and λ ≤ min(m,n); combined with λ ≥ κ = min(m,n), we get **λ = min(m,n)** ✓

**$Q_d$.** It is d-regular, so λ ≤ δ = d and κ ≤ d. The cube is in fact **d-connected**, so κ = λ = **d**.
*Sketch of κ ≥ d:* between any two vertices, route d paths that each fix the differing coordinates in a different cyclic order — the routes stay internally disjoint.

---

# Q14 − Can minimum degree force k-connectedness?

**Question.** Is there f : ℕ → ℕ such that δ(G) ≥ f(k) implies G is k-connected?

**Answer: NO.**

**Counterexample — two blobs glued at one vertex.** Take two copies of the complete graph $K^{r+1}$ and identify **one** vertex of each (call it z).

```
   ▣▣▣▣▣        ▣▣▣▣▣
   ▣ K_{r+1} ▣──z──▣ K_{r+1} ▣
   ▣▣▣▣▣        ▣▣▣▣▣
```

- **Minimum degree = r** — every vertex still sits inside a complete graph on r+1 vertices. Make r as huge as you like.
- **κ = 1** — delete the single vertex z and the graph splits in two.

So given *any* proposed f, take k = 2 and r = f(2). This graph has δ = f(2) but is **not 2-connected** ✓

> **Why the idea fails in principle:** minimum degree is a purely **local** condition — it only sees a vertex's immediate surroundings. Connectivity is **global**. You can always make the neighbourhoods as rich as you please and still leave one narrow bridge between two halves.

**Worth contrasting with Q16:** minimum degree *cannot* force k-connectedness of the whole graph, but it **can** force a highly edge-connected **subgraph**. Passing to a subgraph is what rescues the idea.

---

# Q15 + Formalizing "bounded by" and "forced up by"

Let α, β be graph invariants taking positive integer values.

### Formalizations

**(i) β is bounded above by a function of α:**

$$\exists f:\mathbb{N}\to\mathbb{N} \ \ \forall G: \quad \beta(G) \le f\big(\alpha(G)\big)$$

**(ii) α can be forced up by making β large enough:**

$$\forall k \in \mathbb{N}\ \ \exists m \in \mathbb{N}\ \ \forall G: \quad \beta(G) \ge m \ \Longrightarrow\ \alpha(G) \ge k$$

### (i) ⇒ (ii)

Given k, set **m := 1 + max{ f(1), f(2), …, f(k−1) }** (a finite maximum, so this is well defined).

Suppose β(G) ≥ m but, for contradiction, α(G) ≤ k−1. Then

$$\beta(G) \le f(\alpha(G)) \le \max\{f(1),\dots,f(k-1)\} = m - 1 < m \quad ✗$$

So α(G) ≥ k ✓

### (ii) ⇒ (i)

For each j, apply (ii) with k = j+1 to get mⱼ₊₁ such that β(G) ≥ mⱼ₊₁ ⇒ α(G) ≥ j+1. Read that **contrapositively**:

$$\alpha(G) \le j \ \Longrightarrow\ \beta(G) < m_{j+1}.$$

Define **f(j) := mⱼ₊₁ − 1**. Then α(G) = j gives β(G) ≤ f(j) = f(α(G)) ✓

So **(i) and (ii) say the same thing.**

### (iii) is *not* equivalent

**(iii) α is bounded below by a function of β:**

$$\exists g:\mathbb{N}\to\mathbb{N} \ \ \forall G: \quad \alpha(G) \ge g\big(\beta(G)\big)$$

**Why it's not equivalent: (iii) is trivially true for every pair α, β.** Just take the constant function **g ≡ 1**. Since α takes positive integer values, α(G) ≥ 1 always holds ✓

A statement that holds for *all* invariants cannot be equivalent to (i)/(ii), which genuinely fail for some pairs (e.g. α = connectivity, β = minimum degree — that's exactly Q14).

### The small change that fixes it

Require g to **tend to infinity**:

> **(iii′)** ∃ g with **g(n) → ∞ as n → ∞** such that α(G) ≥ g(β(G)) for all G.

**(ii) ⇒ (iii′).** WLOG the mₖ from (ii) are increasing. Define g(x) := max{ k : mₖ ≤ x } (and g(x) := 1 if no such k). Then β(G) ≥ m_k forces α(G) ≥ k, so α(G) ≥ g(β(G)), and g → ∞ because every mₖ is eventually passed ✓

**(iii′) ⇒ (ii).** Given k, since g → ∞ choose m with g(x) ≥ k for all x ≥ m. Then β(G) ≥ m gives α(G) ≥ g(β(G)) ≥ k ✓

> **The lesson:** "bounded below by a function of β" is vacuous unless the function actually **grows**. The content was never in the inequality — it's in the growth.

---

# Q16 + δ(G) ≥ 2k ⇒ a (k+1)-edge-connected subgraph

**Definition.** H is **(k+1)-edge-connected** if |H| > 1 and every edge cut of H has **at least k+1** edges — equivalently, H − F stays connected whenever |F| ≤ k.

**The strategy.** Pick a **minimal** subgraph satisfying a density condition chosen so that (a) G itself satisfies it, and (b) a small cut would let us pass to a smaller subgraph that still satisfies it — contradicting minimality.

**The right condition.** For a subgraph H, let

$$P(H): \qquad e(H) \;>\; k\big(|H| - 1\big).$$

**Step 1 — G satisfies P.** By handshake, e(G) ≥ δ(G)·n/2 ≥ 2k·n/2 = kn > k(n−1) ✓

**Step 2 — take H minimal.** Among all subgraphs satisfying P, choose one, H, with the **fewest vertices**.

**Step 3 — |H| ≥ 2.** A single vertex has e = 0 and k(1−1) = 0, and 0 > 0 is false, so P fails for single vertices ✓

**Step 4 — H is (k+1)-edge-connected.** Suppose not: there's a partition V(H) = A ⊍ B with both parts non-empty and **at most k** edges crossing. Then

$$e(A) + e(B) \;\ge\; e(H) - k \;>\; k(|H|-1) - k \;=\; k|A| + k|B| - 2k.$$

If **both** H[A] and H[B] failed P, we'd have e(A) ≤ k(|A|−1) and e(B) ≤ k(|B|−1), hence

$$e(A) + e(B) \;\le\; k|A| + k|B| - 2k,$$

flatly contradicting the strict inequality above ✗

So at least one of H[A], H[B] satisfies P. But each has **fewer vertices** than H — contradicting minimality ✗

Therefore no such small cut exists: **H is (k+1)-edge-connected** ✓ ∎

> **Note we proved something stronger than asked:** the argument only used **e(G) > k(n−1)**, not δ(G) ≥ 2k. Minimum degree 2k was just a convenient way to guarantee enough edges. That stronger form is exactly what Q18 asks you to optimise.

---

# Q17 Reflecting on the proof of Theorem 1.4.3

**Theorem 1.4.3 (Mader).** For 0 ≠ k ∈ ℕ, every graph G with d(G) ≥ 4k has a **(k+1)-connected** subgraph H with ε(H) > ε(G) − k.

> ⚠️ **This one I can't answer properly without the book.** The exercise asks you to trace *Diestel's specific induction* — which parts of his statement (∗) survive a change of hypothesis, which adapt, which break. That requires his exact wording in front of you, and I won't reconstruct it from memory and risk telling you something false. **Bring me the page and I'll work through it line by line.**

What I *can* give you is the shape of the answer, which should orient you when you read it.

### (i) Why `e(G′) ≥ γ(|G′| − k)` rather than `ε(G′) > γ − k`

The two look interchangeable, but they behave completely differently under **induction**.

- `ε(G′) > γ − k` is a statement about the **ratio** e/n. When you delete a vertex, both numerator and denominator move, and a ratio hypothesis gives you no clean arithmetic to carry forward.
- `e(G′) ≥ γ(|G′| − k)` is **affine in |G′|**. Deleting a low-degree vertex changes the left side by a known amount and the right side by exactly γ — so the inequality can be checked directly and the induction closes.

The `−k` sitting *inside* the bracket (attached to the vertex count) rather than subtracted from the density is what makes the bookkeeping survive vertex deletion. Expect the proof to break at precisely the step where a vertex is removed and the hypothesis re-applied.

### (ii) Why `m ≥ cₖn − bₖ` rather than `m ≥ cₖn`

The constant offset **bₖ** buys **slack**. With the bare `m ≥ cₖn`, the chain of inequalities at the end of the proof typically closes as an *equality* — giving no contradiction, just a tight case. The additive `−bₖ` makes every step lose a bounded amount, so the final inequality comes out **strict** and the contradiction lands.

This is a common pattern: strengthen the induction hypothesis with a constant term so the induction has room to pay for itself.

**Related:** Q18 is the quantitative version of exactly this question.

---

# Q18 + The smallest b(k)

**Question.** Find the smallest integer b = b(k) such that every graph of order n with **more than kn + b** edges has a (k+1)-edge-connected subgraph.

I can pin this down exactly for k = 1 and bracket it for general k. **The exact value for k ≥ 2 depends on the Theorem 1.4.3 machinery from Q17** — flagging that honestly rather than guessing.

### Upper bound: b(k) ≤ −k

This is exactly what Q16's proof gave us. We showed:

$$e(G) > k(n-1) = kn - k \quad\Longrightarrow\quad \exists \ (k+1)\text{-edge-connected subgraph}.$$

So **b = −k works** ✓

### Lower bound: b(k) ≥ −k(k+1)/2

We exhibit a graph with **many** edges and **no** (k+1)-edge-connected subgraph.

**Construction.** Take $K^k$ (a complete graph on k vertices) and join **every** one of its vertices to **every** vertex of an independent set of size m.

```
   ┌──────────┐
   │   K^k    │═══════ every vertex joined to every ●
   └──────────┘         ●  ●  ●  ●  ●   (independent, m of them)
```

- **n** = k + m, so m = n − k
- **edges** = C(k,2) + km = k(k−1)/2 + k(n−k) = **kn − k(k+1)/2**

**No (k+1)-edge-connected subgraph:**

- Any subgraph H containing one of the m independent vertices v has $\deg_H(v) \le k$, so isolating v is a cut of ≤ k edges → not (k+1)-edge-connected ✗
- Any subgraph avoiding all of them lives inside $K^k$, so |H| ≤ k; a graph on ≤ k vertices has edge-connectivity ≤ k−1 < k+1 ✗

So this graph, with kn − k(k+1)/2 edges, has no such subgraph — meaning the threshold must sit **at least** that high:

$$b(k) \;\ge\; -\frac{k(k+1)}{2}$$

### The verdict

$$-\frac{k(k+1)}{2} \;\le\; b(k) \;\le\; -k$$

**k = 1: exact.** Both bounds equal −1, so **b(1) = −1**. In words: *every graph with more than n−1 edges contains a cycle* (and a cycle is 2-edge-connected). The extremal examples are **trees** — n−1 edges, no cycle at all ✓

**k ≥ 2: a genuine gap.** For k = 2 the bounds are −3 ≤ b(2) ≤ −2. My conjecture is that the lower bound is the truth, i.e.

$$b(k) \;=\; -\frac{k(k+1)}{2},$$

with the K^k-plus-independent-set graph extremal.

**Computational evidence for the conjecture (k = 2).** If b(2) were −2, there would have to exist a graph with **exactly** e = 2n−2 edges and no 3-edge-connected subgraph. I checked **every** such graph exhaustively:

| n | e = 2n−2 | graphs checked | with **no** 3-edge-connected subgraph |
|---|---|---|---|
| 4 | 6 | 1 | 0 |
| 5 | 8 | 45 | 0 |
| 6 | 10 | 3 003 | 0 |

No counterexample exists at these orders, which points to **b(2) = −3 = −k(k+1)/2** ✓ (Evidence, not proof — it doesn't rule out a counterexample at larger n.)

Proving the matching upper bound in general needs a sharper minimality argument than Q16's — one exploiting the fact that when a cut is small, the *smaller* side is tiny and can hold only C(|A|,2) edges rather than k|A|. That refinement is the Theorem 1.4.3 technique. **Flagged for the tutorial.**

---

# Q19 Prove Theorem 1.5.1 (characterisations of a tree)

**Theorem.** The following are equivalent for a graph T:

1. **T is a tree** (connected and acyclic)
2. **Any two vertices of T are linked by a unique path**
3. **T is minimally connected** — connected, but T − e is disconnected for every edge e
4. **T is maximally acyclic** — acyclic, but T + xy contains a cycle for any two non-adjacent x, y

**Strategy: prove the cycle (1) ⇒ (2) ⇒ (3) ⇒ (4) ⇒ (1).** Then any one implies any other by going round.

### (1) ⇒ (2)

**Existence:** T is connected, so some path joins any u, v ✓

**Uniqueness:** this is exactly Property 2 from [[2026-07-24 Preliminaries]] §8. Briefly: if P ≠ Q were two u–v paths, let x be the last vertex they share before splitting and y the first vertex they meet again afterwards. The x–y stretch of P and the x–y stretch of Q meet only at x and y and are different, so gluing them gives a **cycle** — contradicting acyclicity ✗ ✓

### (2) ⇒ (3)

**Connected:** unique paths exist, so paths exist ✓

**Minimal:** let e = xy be any edge. The single edge e *is* an x–y path, and by hypothesis it is the **only** one. If T − e were still connected, it would contain another x–y path — one avoiding e, hence different from e. That's a second x–y path in T ✗

So T − e is disconnected for every e ✓

### (3) ⇒ (4)

**T is acyclic:** suppose T contained a cycle C and let e ∈ E(C). Then T − e is *still connected*: any route that used e can instead go the long way round C. That contradicts minimal connectedness ✗ So T is acyclic ✓

**Maximal:** take non-adjacent x, y. T is connected, so there's an x–y path P. Adding the edge xy gives the cycle P + xy ✓

### (4) ⇒ (1)

**Acyclic** is given ✓

**Connected:** take any x, y.
- If x ~ y, the edge is a path ✓
- If not, then by maximality T + xy contains a cycle C. Since T itself is acyclic, C **must use the new edge xy**. Deleting xy from C leaves an x–y path inside T ✓

So T is connected and acyclic — a tree ✓ ∎

> **How to hold this in your head:** a tree is the exact tipping point between "too few edges" and "too many". Remove any edge and connectivity breaks (3); add any edge and a cycle appears (4). Unique paths (2) is the same balance seen from the middle.

---

# Q20 − Every tree T has at least Δ(T) leaves

**Small fact used below.** *Every tree with ≥ 2 vertices has at least 2 leaves.*
*Why:* take a longest path; each endpoint must be a leaf, since another neighbour would either extend the path (contradicting longest) or close a cycle ✓

**Proof.** Let v be a vertex of maximum degree Δ = Δ(T), with neighbours u₁, …, u_Δ.

**Step 1: T − v has exactly Δ components.** Each uᵢ lands in a component, and **no two uᵢ share one** — if uᵢ and uⱼ were connected in T − v, that path plus the edges uᵢv and vuⱼ would form a **cycle** ✗ And every vertex of T − v connects to some uᵢ (route towards v in T and stop just before). So the components are exactly C₁, …, C_Δ with uᵢ ∈ Cᵢ.

**Step 2: each Cᵢ contains a leaf of T.** Each Cᵢ is a tree.

- **|Cᵢ| = 1.** Then uᵢ's only neighbour in T is v, so $\deg_T(u_i) = 1$ — a leaf ✓
- **|Cᵢ| ≥ 2.** Then Cᵢ has ≥ 2 leaves *of Cᵢ*. Exactly one vertex of Cᵢ is adjacent to v (namely uᵢ — a second one would give a cycle, as in Step 1). So **at least one** leaf w of Cᵢ is not adjacent to v, and then $\deg_T(w) = \deg_{C_i}(w) = 1$ — a leaf of T ✓

**Step 3: count.** The Δ components are disjoint, so the Δ leaves found are distinct:

$$\#\text{leaves}(T) \;\ge\; \Delta(T). \qquad \blacksquare$$

**Check.** The star $K^{1,\Delta}$: centre of degree Δ, and exactly Δ leaves ✓ **tight.**

---

# Q21 A tree with no degree-2 vertex has more leaves than other vertices

**Setup.** Assume |T| ≥ 2. Let

- **L** = number of leaves (degree 1)
- **I** = number of the other vertices — by hypothesis each has degree **≥ 3** (degree 2 is banned, and degree 0 is impossible in a connected graph on ≥ 2 vertices)

So n = L + I, and a tree has n − 1 edges.

### The short proof — pure handshake, no induction

$$\underbrace{2(n-1)}_{\text{handshake}} \;=\; \sum_v \deg(v) \;=\; \underbrace{\sum_{\text{leaves}} \deg}_{=\,L} + \underbrace{\sum_{\text{others}} \deg}_{\ge\, 3I} \;\ge\; L + 3I.$$

Substituting n = L + I on the left:

$$2(L + I - 1) \;\ge\; L + 3I \quad\Longrightarrow\quad 2L + 2I - 2 \;\ge\; L + 3I \quad\Longrightarrow\quad \boxed{L \;\ge\; I + 2}$$

In particular **L > I** — more leaves than non-leaves ✓ ∎

> **That's the whole thing.** Count degrees two ways. The banned degree 2 is exactly the value that would make the inequality balance; forcing every internal vertex to ≥ 3 tips it.

**Check (tight case).** Root r with 3 children, each child with 2 children:

```
        r            deg(r) = 3
      / | \
     a  b  c         deg = 3 each
    /\  /\  /\
   ● ● ● ● ● ●       6 leaves
```

n = 10, edges = 9, Σdeg = 18 = 3 + 3·3 + 6·1 ✓
L = 6, I = 4, and indeed L = I + 2 ✓ **exactly tight.**

---

# Q22 Forest exchange property

**Statement.** Let F, F′ be forests on the **same** vertex set with e(F) < e(F′). Show there is an edge e ∈ F′ such that **F + e is again a forest**.

*(The paste says "F has an edge e" — that's a typo for F′; the edge has to come from the bigger forest.)*

**The key counting identity.** A forest F on n vertices with c(F) components satisfies

$$e(F) = n - c(F).$$

*Why:* each component is a tree, and a tree on nᵢ vertices has nᵢ − 1 edges; summing over components gives n − c ✓

**Proof.** From e(F) < e(F′) and the identity:

$$n - c(F) < n - c(F') \quad\Longrightarrow\quad c(F) > c(F').$$

So **F has strictly more components than F′.**

Now suppose, for contradiction, that **every** edge of F′ has both endpoints inside a single component of F. Then each component of F′ would lie entirely within one component of F — so the F-components would be a **coarsening** of the F′-components, forcing

$$c(F') \ge c(F) \quad ✗$$

contradicting c(F) > c(F′).

Hence some edge **e = xy ∈ F′** has x and y in **different components of F**. Adding it:

- F + e creates no cycle — a cycle through e would need an x–y path in F, but they're in different components ✓

So **F + e is a forest** ✓ ∎

> **What this really is:** the exchange axiom for the **graphic matroid**. The smaller independent set can always be grown using an element of the bigger one. It's the reason the greedy algorithm (Kruskal) finds minimum spanning trees.

---

# Q23 The tree-order is a partial order

**Setup.** Let T be a tree with a fixed **root** r. Since T is a tree, every vertex y has a **unique** r–y path, written rTy. Define

$$x \le y \quad :\Longleftrightarrow\quad x \text{ lies on the path } rTy.$$

### It is a partial order

**Reflexive.** x is an endpoint of rTx, hence on it → x ≤ x ✓

**Antisymmetric.** Suppose x ≤ y and y ≤ x.
Note first: **if x lies on rTy then d(r,x) ≤ d(r,y)**, because the initial stretch of rTy from r to x is itself the (unique) r–x path.
So x ≤ y gives d(r,x) ≤ d(r,y), and y ≤ x gives d(r,y) ≤ d(r,x). Hence **d(r,x) = d(r,y)**.
But on the path rTy there is exactly **one** vertex at distance d(r,y) from r — namely y itself. Since x is on rTy at that distance, **x = y** ✓

**Transitive.** Suppose x ≤ y ≤ z.
Since y lies on rTz, the initial stretch of rTz from r to y is an r–y path — and by uniqueness it **is** rTy. So **rTy is an initial segment of rTz**.
As x lies on rTy, it therefore lies on rTz → **x ≤ z** ✓

So ≤ is a partial order on V(T) ✓

### The claims made about it

**(a) r is the least element.** r lies on every path rTy, so r ≤ y for all y ✓

**(b) The down-set of any vertex is a chain.** For a vertex y,

$$\lceil y \rceil := \{\, x : x \le y \,\} = V(rTy),$$

the vertex set of a single path. Along a path the vertices are strictly increasing in distance from r, so any two are comparable — **it's a chain**, in fact a finite linear order of length d(r,y) ✓

**(c) Any two vertices have a greatest lower bound.** Given x, y, the paths rTx and rTy share an initial stretch; let **z** be their **last common vertex**. Then z ≤ x and z ≤ y, and any w with w ≤ x and w ≤ y lies on both paths, hence on the common stretch, hence w ≤ z. So z = x ∧ y ✓

**(d) The maximal elements are exactly the leaves** (other than r when |T| = 1). If y is not a leaf, it has a neighbour further from r, which lies strictly above it; if y is a leaf ≠ r, nothing lies beyond ✓

**(e) Every connected subgraph (subtree) has a least element.** Take the vertex of the subtree closest to r; uniqueness of paths makes it comparable to — and below — all the others ✓ ∎

> **Picture it as gravity.** Hang the tree from r. Then x ≤ y means "x is on the way down from the root to y" — i.e. x is an ancestor of y. Everything above is the familiar ancestor/descendant order on a rooted tree.

---

## Status summary

| Q | Topic | Status |
|---|---|---|
| 1 | edges of Kⁿ | ✅ complete |
| 2 | d-cube invariants | ✅ complete |
| 3 | cycle of length ≥ √k | ✅ complete |
| 4 | tightness of Prop 1.3.2 | ✅ complete |
| 5 | distance layers | ✅ complete |
| 6 | rad ≤ diam ≤ 2rad | ✅ complete |
| 7 | Moore bound, min degree | ✅ complete |
| 8 | girth 5 ⇒ δ = o(n) | ✅ complete (sharp: δ ≤ √(n−1)) |
| 9 | path or cycle ≥ min{2δ, n} | ✅ complete |
| 10 | diameter k, min degree d | ✅ complete (both directions) |
| 11 | components partition V | ✅ complete |
| 12 | 2-connected ⇒ cycle | ✅ complete |
| 13 | κ and λ of standard families | ✅ complete |
| 14 | min degree can't force k-connectivity | ✅ complete |
| 15 | formalizing invariant bounds | ✅ complete |
| 16 | δ ≥ 2k ⇒ (k+1)-edge-conn. subgraph | ✅ complete |
| 17 | reflecting on Thm 1.4.3's proof | ⚠️ **needs the book** — shape given |
| 18 | smallest b(k) | ⚠️ **exact for k=1**; bracketed for k ≥ 2 |
| 19 | Theorem 1.5.1 | ✅ complete |
| 20 | ≥ Δ(T) leaves | ✅ complete |
| 21 | more leaves than others | ✅ complete (short proof, no induction) |
| 22 | forest exchange | ✅ complete |
| 23 | tree-order | ✅ complete |

## To bring to the tutorial

- [ ] **Q17** — bring the page with Theorem 1.4.3's proof and statement (∗); I'll walk the induction with you
- [ ] **Q18** — the exact b(k) for k ≥ 2; my bracket is −k(k+1)/2 ≤ b(k) ≤ −k
- [ ] Confirm the numbering of Prop 1.3.2 / Thm 1.3.4 / Thm 1.4.3 / Thm 1.5.1 matches your edition

