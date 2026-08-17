---
tags: [academics, graph-theory, tutorial]
type: tutorial
date: 2026-07-31
seq: 6
class: 4
---

# 6 · 2026-07-31 — Tutorial 1

**◀ Previous:** [[2026-07-29 Matchings 2 — Berge and König]]  ·  **Hub:** [[Graph Theory]]  ·  **Next ▶** [[2026-08-10 Matchings in Bipartite Graphs]]

**Six problems.** Every proof below is broken into numbered **Claims** proved separately, then combined.

---

## Symbols

| Symbol | Meaning |
|---|---|
| **Qₙ** | the n-dimensional hypercube |
| **girth** | length of the **shortest cycle** |
| **induced path** | a path with **no chords** — the subgraph induced on its vertices is exactly the path |
| **δ(G)** | minimum degree · **k-regular** = every vertex has degree exactly k |
| **d(u,v)** | length of a shortest u–v path |

---

# Q1 — The hypercube Qₙ

> **Definition.** Qₙ has vertex set = all **n-tuples of 0s and 1s**; two tuples are adjacent iff they **differ in precisely one coordinate**.

```
 Q1:  0 —— 1          Q2:   00 —— 01          Q3: the cube on
                             |      |              000 001 011 010
                            10 —— 11              100 101 111 110
```

> Fully worked in [[Assignment 1]] Q2 as well — this is the tutorial version with the extra planarity part.

## (i) Number of vertices = 2ⁿ

Each of the n coordinates is chosen independently as 0 or 1 → **2ⁿ** tuples ✓

## (ii) Number of edges = n·2ⁿ⁻¹

**Claim 1.1 — Qₙ is n-regular.**
From a tuple x you reach a neighbour by flipping exactly **one** coordinate. There are n coordinates, and flipping different ones gives different tuples. So **deg(x) = n** for every x ✓

**Combining with the handshake lemma:**

$$2m = \sum_v \deg(v) = 2^n \cdot n \quad\Longrightarrow\quad m = \frac{n \cdot 2^n}{2} = n\,2^{\,n-1}$$

*(My notes wrote 2ⁿ·n / 2 — the same number ✓)*

**Check.** Q₃: 3·2² = 12, and a cube has 12 edges ✓

## (iii) Girth = 4 (for n ≥ 2)

**Claim 1.2 — Qₙ has no cycle of length 3.**
Follows from (iv) below: Qₙ is bipartite, so it has **no odd cycle at all** ✓

**Claim 1.3 — Qₙ has a cycle of length 4.**
Flip the **last two significant bits** in the four possible ways, leaving everything else fixed:

$$00\ldots 00 \;\to\; 00\ldots 01 \;\to\; 00\ldots 11 \;\to\; 00\ldots 10 \;\to\; 00\ldots 00$$

Consecutive tuples differ in exactly one bit ✓ and all four are distinct ✓ — a 4-cycle.

**Combining:** no cycle shorter than 4 exists, and a 4-cycle does. **girth(Qₙ) = 4** for n ≥ 2 ✓
*(Q₁ = K₂ has no cycle at all, so its girth is ∞.)*

> This is the "last 2 sig bits" note on my page — that's exactly the square you get by wiggling two coordinates.

## (iv) Qₙ is bipartite (hence all cycles are even)

**Claim 1.4 — the parity colouring works.**
Colour each tuple by the **parity of its number of 1s**:

$$X = \{\,x : x \text{ has an \textbf{even} number of 1s}\,\}, \qquad Y = \{\,x : \textbf{odd}\,\}.$$

Every edge flips **exactly one** coordinate, which changes the count of 1s by exactly ±1 — so it **always flips the parity**. Therefore every edge joins X to Y, and **no edge lies inside X or inside Y** ✓

So Qₙ is bipartite. By the theorem from [[2026-07-24 Preliminaries]] §9, **a bipartite graph has no odd cycle** — so all cycles of Qₙ are of **even length** ✓

## (v) Qₙ has a Hamiltonian cycle (n ≥ 2)

**Proof by induction on n**, using the hint about combining cycles.

**Base n = 2.** Q₂ *is* the 4-cycle 00–01–11–10–00 ✓

**Inductive step.** Assume Qₙ has a Hamiltonian cycle C.

**Claim 1.5 — Qₙ has a Hamiltonian *path*.**
Delete any one edge of C. What remains is a path visiting every vertex, say from **a** to **b** ✓ Call it P.

**Claim 1.6 — Qₙ₊₁ is two copies of Qₙ joined by a perfect matching.**
Split the (n+1)-tuples by their **first** coordinate: those starting **0** and those starting **1**. Within each half, the remaining n coordinates behave exactly like Qₙ. Across the halves, `0x` is adjacent to `1x` and nothing else — a perfect matching of "twin" edges ✓

**Combining 1.5 and 1.6 — build the cycle.**

```
 0-copy:   0a ──────── P ────────► 0b
                                    │  twin edge 0b–1b
 1-copy:   1a ◄─────── P ────────── 1b
            │
            └── twin edge 1a–0a ────┘  back to start
```

Traverse `0a → P → 0b`, cross the twin edge to `1b`, traverse P **backwards** to `1a`, then cross the twin edge back to `0a`.

Every vertex of both copies is used **exactly once**, and the walk closes ✓ That's a Hamiltonian cycle of Qₙ₊₁ ∎

**Consequence:** the **circumference** of Qₙ is 2ⁿ — the largest possible.

## ★ Is Q₄ planar? — **No**

**Claim 1.7 — a simple bipartite planar graph with n ≥ 3 satisfies m ≤ 2n − 4.**
For a planar graph, Euler's formula gives n − m + f = 2. Each face is bounded by at least **4** edges (bipartite ⇒ girth ≥ 4, no triangles), and each edge borders at most 2 faces, so 4f ≤ 2m, i.e. f ≤ m/2. Substituting:

$$2 = n - m + f \le n - m + \frac{m}{2} = n - \frac{m}{2} \quad\Longrightarrow\quad m \le 2n - 4 \;✓$$

**Combining with the counts for Q₄:** n = 2⁴ = **16**, m = 4·2³ = **32**.

$$2n - 4 = 2(16) - 4 = 28 \quad\text{but}\quad m = 32 > 28 \;✗$$

**Q₄ is not planar** ✓

> **Note the trap.** The *general* planar bound m ≤ 3n − 6 gives 42 here, and 32 ≤ 42 — so the general bound says nothing. You **must** use the bipartite version. Q₃ (the ordinary cube) *is* planar: n = 8, m = 12, and 12 ≤ 2(8) − 4 = 12 ✓ exactly at the limit.

---

# Q2 — A k-regular graph of girth 5 has at least k² + 1 vertices

**Setup.** G is k-regular (every vertex has degree exactly k) with **girth ≥ 5**, meaning **no cycle of length 3 or 4**.

Fix any vertex **v**, and write **N = N(v)**, so |N| = k.

### Claim 2.1 — N is an independent set

If two neighbours u, u′ ∈ N were adjacent, then **v–u–u′–v** is a **triangle** (cycle of length 3) ✗ contradicting girth ≥ 5 ✓

### Claim 2.2 — each u ∈ N has at least k−1 neighbours outside {v} ∪ N

u has degree exactly k. One of its edges goes to v. By **Claim 2.1**, none of its other edges goes into N. So all **k − 1** remaining edges lead to vertices outside {v} ∪ N ✓

### Claim 2.3 — those outer neighbourhoods are pairwise disjoint

Suppose u₁ ≠ u₂ in N shared an outer neighbour w. Then

$$v \to u_1 \to w \to u_2 \to v$$

is a **4-cycle** ✗ contradicting girth ≥ 5 ✓

### Combining the claims — count the vertices

The three groups below are pairwise disjoint, so we may simply add their sizes:

| group | size | guaranteed by |
|---|---|---|
| {v} | 1 | — |
| N(v) | k | k-regularity |
| outer neighbours of N | k(k−1) | Claims 2.2 and 2.3 |

$$n \;\ge\; 1 + k + k(k-1) \;=\; 1 + k + k^2 - k \;=\; \boxed{k^2 + 1} \qquad \blacksquare$$

**Sharpness.** The **Petersen graph** is 3-regular with girth 5 and has exactly 10 = 3² + 1 vertices ✓ **The bound is tight.**

> Same argument as [[Assignment 1]] Q8, where it gave δ ≤ √(n−1). Here it's read in the other direction: fix the degree, and the vertex count is forced up.

---

# Q3 — Connected, simple, not complete ⇒ contains an induced path of length two

> An **induced path of length two** means three vertices a, b, c with edges **ab** and **bc** but **no edge ac**.

### Claim 3.1 — there exist two non-adjacent vertices

G is **not complete**, so by definition some pair of vertices u, w has **no edge** between them ✓

### Claim 3.2 — a shortest u–w path has length at least 2

G is **connected**, so a u–w path exists. It cannot have length 1, since that would be the edge uw, which Claim 3.1 says is absent. So **d(u,w) ≥ 2** ✓

### Claim 3.3 — the first three vertices of a shortest path form an induced P₃

Let $u = x_0, x_1, x_2, \dots$ be a **shortest** u–w path (it has at least three vertices by Claim 3.2).

- **x₀x₁ is an edge** ✓ (consecutive on the path)
- **x₁x₂ is an edge** ✓ (consecutive on the path)
- **x₀x₂ is NOT an edge:** if it were, we could skip x₁ and get a strictly shorter u–w path ✗ contradicting shortest ✓

So x₀ x₁ x₂ is an induced path of length two ✓

### Combining

Claims 3.1 and 3.2 supply a shortest path with ≥ 3 vertices; Claim 3.3 extracts the induced P₃ from its first three ∎

> **Where each hypothesis is used:** *not complete* gives the missing edge; *connected* guarantees a path between those two vertices exists at all. Drop either and the result fails — Kₙ has no induced P₃, and a graph of two isolated vertices has no path.

---

# Q4 — Any two longest paths in a connected graph share a vertex

### ⚠️ Correction to my notes

My page says *"2 longest paths are of length m, m or m, m−1 — I'm not sure"*. **It's always m, m.** "Longest" means *maximum length*, and a maximum is a single number — so **both** longest paths have exactly the same length m. There is no m, m−1 case.

My step 2 says *"a path from b/w these 2 paths don't exist"*. That's backwards: connectivity **guarantees** such a path **does** exist, and that's precisely what produces the contradiction.

---

**Setup.** Let P and Q be two longest paths, each of length **m**. Suppose for contradiction they are **vertex-disjoint**.

### Claim 4.1 — a connecting path exists

G is connected, so there is a path from a vertex of P to a vertex of Q. Choose a **shortest** such path R, joining **p ∈ P** to **q ∈ Q**.

Because R is shortest, its **interior vertices touch neither P nor Q** — otherwise we could cut R short at the first touch ✓ Let R have length **r ≥ 1**.

```
   P: ●———●———●———p———●———●          length m
                  │
                  R  (length r ≥ 1, internally disjoint)
                  │
   Q: ●———●———q———●———●———●          length m
```

### Claim 4.2 — from p, one side of P has length at least ⌈m/2⌉

The vertex p splits P into two stretches, running from p to each end of P. Their lengths add up to **m**, so the **longer** of the two is at least **⌈m/2⌉** ✓ Call that stretch **P₁**.

By the identical argument on Q, take the longer stretch **Q₁** from q, of length ≥ **⌈m/2⌉** ✓

### Claim 4.3 — gluing gives a genuine path

Consider **P₁ + R + Q₁**: walk from the far end of P₁ down to p, cross R to q, then out along Q₁.

Is it a path (no repeated vertices)?

- P₁ ⊆ P and Q₁ ⊆ Q are **disjoint** — that's our assumption ✓
- R's interior meets neither P nor Q, by Claim 4.1 ✓
- R's endpoints are p ∈ P₁ and q ∈ Q₁, each used once ✓

So no vertex repeats ✓

### Combining the claims — the contradiction

$$\text{length}(P_1 + R + Q_1) \;=\; |P_1| + r + |Q_1| \;\ge\; \left\lceil \tfrac{m}{2} \right\rceil + r + \left\lceil \tfrac{m}{2} \right\rceil \;\ge\; m + r \;\ge\; m + 1.$$

*(using ⌈m/2⌉ + ⌈m/2⌉ ≥ m, and r ≥ 1)*

We have built a path **strictly longer than m** — but m was the length of a **longest** path ✗

**Contradiction.** So P and Q cannot be disjoint: **any two longest paths share a vertex** ∎

> **Where connectivity is essential:** in a disconnected graph the result is false. Two disjoint copies of P₃ give two longest paths with no vertex in common.

---

# Q5 — A shortest (a,b) path is always an induced path

> **To prove:** if P is a shortest a–b path, then P has **no chords** — no edge of G joins two non-consecutive vertices of P.

**Setup.** Let $P = v_0 v_1 \cdots v_k$ with $v_0 = a$, $v_k = b$, of length k = d(a,b).

### Claim 5.1 — a chord would create a shortcut

Suppose a chord $v_i v_j$ exists with **j > i + 1** (non-consecutive). Build the walk

$$v_0 \to v_1 \to \cdots \to v_i \;\xrightarrow{\ \text{chord}\ }\; v_j \to v_{j+1} \to \cdots \to v_k .$$

Count its edges:

$$\underbrace{i}_{v_0 \to v_i} \;+\; \underbrace{1}_{\text{the chord}} \;+\; \underbrace{(k - j)}_{v_j \to v_k} \;=\; k - (j - i) + 1.$$

### Claim 5.2 — the shortcut is strictly shorter

Since j > i + 1, we have **j − i ≥ 2**, hence

$$k - (j-i) + 1 \;\le\; k - 2 + 1 \;=\; k - 1 \;<\; k \;✓$$

Also, this walk uses only vertices of P, each **at most once** (we go up to vᵢ, jump to vⱼ, continue upward), so it is a genuine **path** ✓

### Combining

Claims 5.1 and 5.2 produce an a–b path of length < k. But k = d(a,b) is the **minimum** possible ✗

**Contradiction.** So no chord exists, and P is **induced** ∎

**Concrete check.** In C₄ = a–b–c–d–a, the shortest a–c path is a–b–c, length 2, with no chord ac (there isn't one) ✓ Now add the chord ac: the shortest a–c path becomes the single edge, length 1 — and *that* has no chord either ✓

> **Q3 and Q5 are the same observation** used twice: *a shortest path can never contain a shortcut, because a shortcut is exactly what "shortest" forbids.* Q3 applies it to the first three vertices; Q5 applies it to every pair.

---

# Q6 — Pairwise-intersecting intervals share a common point

> **Statement.** Let I₁, …, I_N be intervals on the real line such that **every pair intersects**. Then **all** of them have a point in common.

*(My notes guessed "**eli property?**" — the word is **Helly property**. This is the 1-dimensional case of Helly's theorem.)*

**Setup.** Write each interval in closed form $I_i = [a_i,\, b_i]$, and define

$$a^{*} := \max_i a_i \quad(\text{the rightmost left endpoint}), \qquad b^{*} := \min_i b_i \quad(\text{the leftmost right endpoint}).$$

### Claim 6.1 — a* ≤ b*

Let **p** be an index achieving the maximum, so $a^{*} = a_p$, and **q** an index achieving the minimum, so $b^{*} = b_q$.

By hypothesis intervals $I_p$ and $I_q$ **intersect**, so some point t lies in both:

$$a_p \le t \le b_p \quad\text{and}\quad a_q \le t \le b_q .$$

From the first, $a_p \le t$; from the second, $t \le b_q$. Chaining:

$$a^{*} = a_p \;\le\; t \;\le\; b_q = b^{*} \;✓$$

*(This is the **only** place the pairwise hypothesis is used — and one well-chosen pair is all it takes.)*

### Claim 6.2 — a* lies in every interval

Take any interval $I_i = [a_i, b_i]$. Then

- $a_i \le a^{*}$ — because a\* is the **maximum** of all left endpoints ✓
- $a^{*} \le b^{*} \le b_i$ — the first step by **Claim 6.1**, the second because b\* is the **minimum** of all right endpoints ✓

Together: $a_i \le a^{*} \le b_i$, so $a^{*} \in I_i$ ✓

### Combining

Claim 6.2 holds for **every** i, so the single point **a\*** lies in all the intervals ∎

```
  I₁  ├──────────────────┤
  I₂        ├───────────────────┤
  I₃    ├────────────┤
                  ↑
              a* = rightmost left endpoint — inside all of them
```

**Worked example.** [0, 5], [3, 8], [2, 6]. Pairwise intersecting ✓
a\* = max{0, 3, 2} = **3**; b\* = min{5, 8, 6} = **5**. Since 3 ≤ 5 ✓, the point **3** lies in all three ✓

> ⚠️ **Closedness matters.** For open intervals the result can fail: (0,1) and (1,2) don't intersect, but consider (0,1), (0.5, 1), (0.9, 1) — those do share points, fine. The genuine failure needs infinitely many: (0, 1/k) for k = 1, 2, 3, … pairwise intersect, yet **no** point is in all of them. So the theorem needs either **closed** intervals or **finitely many**.

> **The "tree?" note on my page:** this generalises beautifully — **subtrees of a tree** also have the Helly property (pairwise-intersecting subtrees share a vertex). That's the fact underpinning **chordal graphs**, which show up in the perfect-graphs unit.

---

## Takeaways

1. **Qₙ:** 2ⁿ vertices, n-regular, n·2ⁿ⁻¹ edges, diameter n, girth 4, Hamiltonian. Bipartite by **parity of the number of 1s**.
2. **Q₄ is not planar** — and you need the *bipartite* bound m ≤ 2n − 4 to see it; the general 3n − 6 bound is too weak.
3. **Girth 5 forces room:** n ≥ k² + 1, tight at the Petersen graph. Same count as [[Assignment 1]] Q8, read the other way.
4. **"Shortest" forbids shortcuts.** Q3 and Q5 are both this one idea — a chord would shorten the path.
5. **Two longest paths must meet**, because otherwise you glue half of each onto a connecting path and beat the maximum.
6. **Helly in 1D:** the rightmost left endpoint is the common point, and you only need **one** well-chosen pair to prove it.
7. **Extremal quantities** (a\*, b\*, longest, shortest) are the workhorse of this entire tutorial.

---

## Doubts / to revisit

- [ ] My Q4 note guessed lengths "m, m−1" — corrected above: both longest paths have length exactly m.
- [ ] My Q4 step 2 said the connecting path "doesn't exist" — it's the opposite; connectivity guarantees it does.
- [ ] The Helly property for **subtrees of a tree** (the "tree?" note) — comes back with chordal graphs.
