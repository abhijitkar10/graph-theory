---
tags: [academics, graph-theory, lecture]
date: 2026-07-24
seq: 1
class: 1
---

# 1 · 2026-07-24 — Preliminaries

**◀ Previous:** *(none — first note)*  ·  **Hub:** [[Graph Theory]]  ·  **Next ▶** [[2026-07-24 Long Path Theorem]]

**Covered:** clique, edge density & average degree, "large average degree ⇒ dense subgraph", the δ ≥ k family of lemmas, maximal vs longest paths, trees, bipartite graphs.

**Homework set in class:** Diestel Ch. 1 — 23 problems.

---

## 0. Symbols used today

| Symbol | Meaning |
|---|---|
| **n** | number of **vertices** |
| **m** | number of **edges** |
| **δ(G)** | *minimum* degree — smallest number of edges touching any one vertex |
| **Δ(G)** | *maximum* degree |
| **deg(v)** | degree of v — how many edges touch it |
| **N(v)** | the **neighbourhood** of v — the set of vertices joined to v by an edge |
| **u ~ v** | u is adjacent to v |
| **V(P), E(P)** | the vertex set / edge set of a path P |
| **length of a path or cycle** | number of **edges** in it |

> A **simple graph** has no self-loops and no repeated edges. Consequence used constantly: **v ∉ N(v)**, so a vertex is never its own neighbour.

---

## 1. Clique *(the "clique???" in my notes)*

> A **clique** is a set of vertices that are **all** pairwise adjacent — every possible edge among them is present.

A clique on r vertices is a copy of the complete graph **Kᵣ** sitting inside G.

```
K3 (triangle)        K4
   a                a———b
  / \               |\ /|
 b———c              | X |
                    |/ \|
                    c———d
```

- **Clique number ω(G)** = size of the largest clique in G.
- Finding it is **NP-hard**. (Compare: the *maximum independent set* is a clique in the complement graph.)
- **Independent set** = the opposite: a set of vertices with **no** edges among them. This is the notion needed for bipartite graphs in §8.

---

## 2. Does "many edges" force connectedness?

**Question from class:** a graph has many edges — can we conclude it's connected?

**Answer: NO.** The counterexample drawn in class:

```
   ┌─────────────┐
   │ ▧▧▧▧▧▧▧▧▧▧ │        ● ← isolated vertex
   │ ▧ K_{n-1} ▧ │
   └─────────────┘
    tons of edges          δ(G) = 0
```

Take **Kₙ₋₁** (a complete graph on n−1 vertices, so C(n−1,2) edges — a huge number) and add **one isolated vertex**. The graph has masses of edges but is **disconnected**, and **δ(G) = 0**.

**Moral:** *many edges* is a **global/average** condition. It says nothing about any **individual** vertex. One lonely vertex ruins connectedness and drags δ to 0, no matter how dense the rest is. This is exactly why the next section is interesting — we have to *hunt for a subgraph* rather than hope the whole graph is nice.

### But there IS a threshold (bonus, worth knowing)

> If **m > C(n−1, 2)** then G **must** be connected.

**Proof.** Suppose G is disconnected. Then we can split the vertices into two non-empty groups, sizes **a** and **n−a**, with **no edges between them** (put one component on one side, the rest on the other). All edges live inside one group or the other, so

$$m \;\le\; \binom{a}{2} + \binom{n-a}{2}.$$

This expression is largest when the split is as **lopsided** as possible, i.e. a = 1 (check a = 1: C(1,2) + C(n−1,2) = 0 + C(n−1,2); any more balanced split gives less). So **m ≤ C(n−1,2)**.

We assumed m > C(n−1,2), a contradiction. So G is connected. ∎

Notice Kₙ₋₁ + isolated vertex has **exactly** C(n−1,2) edges — it sits right at the threshold and is disconnected, so the bound is **sharp** (can't be improved).

---

## 3. Handshake lemma, average degree, edge density

### Handshake Lemma

$$\sum_{v \in V} \deg(v) \;=\; 2m$$

**Why?** Count the pairs (vertex, edge touching it). Going **vertex by vertex** gives Σ deg(v). Going **edge by edge**, each edge has exactly **2 endpoints**, so it gets counted exactly twice, giving 2m. Same quantity counted two ways. ∎

> Tiny check: triangle K₃ has 3 edges. Each vertex has degree 2. Σ deg = 2+2+2 = 6 = 2 × 3 ✓

### Average degree

$$d_{\text{avg}} \;=\; \frac{1}{n}\sum_v \deg(v) \;=\; \frac{2m}{n}$$

### Edge density

$$\varepsilon(G) \;=\; \frac{m}{n} \;=\; \frac{1}{2}\, d_{\text{avg}}$$

**So edge density is just half the average degree.** They're the same information in different clothes. (Class wrote this as `m/n = edge density = ½ · avg degree`.)

---

## 4. ★ Theorem — large edge density gives a subgraph with large minimum degree

**The motivating question:** average degree being large is only an *average* — §2 showed the graph can still contain a degree-0 vertex. But can we always **dig out a piece** of the graph where *every* vertex has high degree?

> **Theorem.** If the edge density of G is **k** (that is, m/n = k), then there exists a subgraph **H ⊆ G** with **δ(H) ≥ k**.

### The idea

The bad vertices are the low-degree ones. So **throw them away.** The worry is that deleting vertices might destroy the density we're relying on. The key insight from class:

> *"If I remove vertices, remove such that you don't destroy more than (k−1) edges."*

Deleting a vertex costs us **1 vertex** but only **deg(v) edges**. If deg(v) < k, we're removing proportionally *fewer edges than the density demands* — so the density **goes up**, not down.

### Proof — four claims, then combine

| | Claim |
|---|---|
| **A** | deleting a low-degree vertex never **decreases** the density |
| **B** | the process must **stop** (finiteness) |
| **C** | it cannot strip the graph **bare** |
| **D** | when it stops, **δ(H) ≥ k** by definition of "stops" |

Repeatedly delete any vertex of degree **< k**:

$$G \xrightarrow{\;-v_1\;} G_1 \xrightarrow{\;-v_2\;} G_2 \xrightarrow{\;-v_3\;} \cdots$$

**Claim A — deletion never decreases the density.** Say the current graph has n vertices, m edges, density m/n ≥ k, and v has deg(v) ≤ k−1. The new graph has n−1 vertices and m − deg(v) ≥ m − (k−1) edges. Its density is

$$\frac{m - \deg(v)}{n-1} \;\ge\; \frac{m - k + 1}{n - 1} \;\ge\; \frac{nk - k + 1}{n-1} \;=\; \frac{k(n-1) + 1}{n-1} \;=\; k + \frac{1}{n-1} \;>\; k.$$

(The middle step used m ≥ nk, which is just m/n ≥ k rearranged.) So density stays **> k** forever after. ✓

**Claim B — the process stops.** Each step removes a vertex, and G is finite, so we can't go forever ✓

**Claim C — it can't strip the graph bare.** A graph on 1 vertex has 0 edges, density 0/1 = 0, which is **< k**. But Step A guarantees density stays ≥ k. So the process must halt **while a real graph is still standing** (in fact with m ≥ kn > 0, so it still has edges).

**Claim D — read off the answer.** The process halts precisely when **no vertex has degree < k**. Call that graph **H**. Every vertex of H has degree ≥ k, i.e. **δ(H) ≥ k** ✓

**Combining A–D:** the process runs (B), never spoils the density (A), leaves a real graph standing (C), and what's standing has minimum degree ≥ k (D). ∎

> **Watch out — a genuine subtlety.** "deg(v)" in Claim A means the degree *in the current graph*, not in the original G. Degrees shrink as we delete, so a vertex that looked fine early can become deletable later. The proof handles this automatically because we re-examine the graph at every step.

---

## 5. Maximal vs Longest — a distinction that matters

> A set **S** is **maximal** with respect to a property **(P)** if there is **no set Q with Q ⊋ S** that also satisfies (P).

In words: *maximal = you cannot extend it any further.* This is **not** the same as *biggest*.

### Maximal path

A path is **maximal** if you cannot add a vertex to either end.

```
 a₁ ●———————————————● a_k
     neighbours of the endpoints have to be ON the path,
     otherwise you could extend → not maximal
```

### The crucial difference

| | **Maximal** path | **Longest** path |
|---|---|---|
| Meaning | can't be extended | no longer path exists anywhere |
| How to find | greedy: keep extending until stuck | search everything |
| Cost | **polynomial time** | **NP-complete** (via Hamiltonian path) |

**Example showing they differ.** In this graph:

```
a ——— b ——— c ——— d ——— e
      |
      f
```

The path **f – b – a** is *maximal* (f has no other neighbour; a has no other neighbour) but has length 2. The *longest* path is a–b–c–d–e, length 4. So **maximal ≠ longest**.

> **Why this matters for proofs:** every argument today only needs "**can't be extended**", which a *maximal* path already gives. That's a much cheaper object to grab. Every "longest path" argument below works verbatim with "maximal path" — and a maximal path always exists (just start anywhere and keep walking).

---

## 6. The δ ≥ k family of lemmas

All three use the same weapon: **take a maximal path, look at its last vertex.**

### Lemma A — δ(G) ≥ k ⇒ G has a path with at least k+1 vertices

*(equivalently, a path of length ≥ k)*

**Proof.** Let P = v₁ v₂ … vᵣ be a **maximal** path, with last vertex **vᵣ**.

Since P is maximal, **every neighbour of vᵣ already lies on P** (otherwise we'd extend P by that neighbour). So:

$$V(P) \;\supseteq\; \underbrace{\{v_r\}}_{1} \;\cup\; \underbrace{N(v_r)}_{\ge\, k}$$

These two pieces don't overlap, because G is **simple** — vᵣ is not its own neighbour. Therefore

$$|V(P)| \;\ge\; 1 + k \;=\; k+1. \qquad \blacksquare$$

> Concrete: δ ≥ 3 means vᵣ has ≥ 3 neighbours, all on P, plus vᵣ itself → P has ≥ 4 vertices, length ≥ 3.

### Lemma A again, by induction *(the proof my notes started)*

**Claim.** For every k ≥ 1: if δ(G) ≥ k then G has a path of length k.

**Base case k = 1.** δ ≥ 1 means every vertex has at least one edge, so an edge exists, which *is* a path of length 1 ✓

**Inductive hypothesis.** Suppose the claim holds for k: every graph with δ ≥ k has a path of length k.

**Inductive step.** Let G have **δ(G) ≥ k+1**. Since k+1 > k, we also have δ(G) ≥ k, so the hypothesis gives a path **P = v₀ v₁ … vₖ** of length k. We must stretch it to length k+1.

- **If vₖ has a neighbour off P** — attach it. Path of length k+1 ✓
- **If not** — every neighbour of vₖ lies on P. Its neighbours can only be among **v₀, …, vₖ₋₁**, which is just **k vertices**. But deg(vₖ) ≥ δ ≥ **k+1**. We'd need k+1 distinct neighbours to fit into k slots — **impossible**.

So the second case never happens, the extension always works, and G has a path of length k+1. ∎

*(My notes stopped at "By inductive hypothesis since δ(G) ≥ k, ∃ a path of length k" — the missing piece is exactly the pigeonhole above.)*

### Lemma B — δ(G) ≥ k with k ≥ 2 ⇒ G contains a cycle

**Proof.** Take a maximal path P = v₁ … vᵣ. All of vᵣ's neighbours lie on P (maximality), and there are **at least 2** of them.

One of them is vᵣ₋₁, its neighbour along the path. Since deg(vᵣ) ≥ 2, there is a **second** neighbour **vᵢ** with **i < r−1**.

Now walk: **vᵢ → vᵢ₊₁ → … → vᵣ → vᵢ.**

```
 v_i ——— v_{i+1} ——— … ——— v_{r-1} ——— v_r
  └──────────────────────────────────────┘
              the extra edge v_r ~ v_i
```

Path edges get us from vᵢ to vᵣ; the extra edge closes it. Vertices are distinct (they came from a path). Length = (r − i) + 1 ≥ **3** since i ≤ r−2. A genuine cycle. ∎

### Lemma C — δ(G) ≥ k ⇒ G contains a cycle of length at least k+1

**Proof.** Maximal path P = v₁ … vᵣ again, all of N(vᵣ) on P.

Let **vᵢ = the furthest neighbour of vᵣ along P** — i.e. the neighbour with the **smallest index** (furthest back from the end).

Then every neighbour of vᵣ lies in the block **{vᵢ, vᵢ₊₁, …, vᵣ₋₁}**. Count the slots in that block: **r − i**. Count the neighbours that must fit: **≥ k**. So

$$r - i \;\ge\; k.$$

Close the cycle **vᵢ → vᵢ₊₁ → … → vᵣ → vᵢ**. Its length is (r − i) + 1 ≥ **k + 1**. ∎

This is the counting my notes tabulated:

| vᵣ joined to… | edges used | vertices used |
|---|---|---|
| 1st neighbour | 1 | 2 |
| 2nd neighbour | 2 | 3 |
| (k−1)ᵗʰ neighbour | k−1 | k |
| kᵗʰ neighbour (vᵢ) | k | k+1 |

Up to vᵢ it's a path; **then add the edge vᵢ → vᵣ to make it a cycle.**

---

## 7. ★ Exercise — δ(G) ≥ 3 ⇒ G contains an **even** cycle

*(Stated in class without proof. Here's the proof.)*

**Why it's not obvious:** Lemma C gives a cycle of length ≥ 4, but says nothing about **parity**. We need to manufacture *several* cycles and argue at least one has even length.

**Structure:** Claim 7.1 builds three cycles from three neighbours; Claim 7.2 shows they can't all be odd.

**Claim 7.1 — three neighbours of an endpoint give three cycles.**

Take a **maximal path** P = v₀ v₁ … vₖ. All of v₀'s neighbours lie on P, and δ ≥ 3 means there are **at least 3** of them:

$$v_0 \sim v_i,\quad v_0 \sim v_j,\quad v_0 \sim v_l \qquad\text{with } 0 < i < j < l \le k.$$

Each **pair** of these gives a cycle. Using vᵢ and vⱼ:

$$v_0 \to v_i \to v_{i+1} \to \cdots \to v_j \to v_0$$

Its length = 1 (edge v₀vᵢ) + (j − i) (path edges) + 1 (edge vⱼ v₀) = **(j − i) + 2**.

So the three cycles have lengths:

| cycle from | length |
|---|---|
| vᵢ , vⱼ | (j − i) + 2 |
| vⱼ , vₗ | (l − j) + 2 |
| vᵢ , vₗ | (l − i) + 2 |

Write **a = j − i** and **b = l − j**. Then **l − i = a + b**, and the three lengths are

$$a+2, \qquad b+2, \qquad a+b+2.$$

**Claim 7.2 — the three lengths cannot all be odd.**

Suppose they were. Adding 2 doesn't change parity, so that needs **a, b, and a+b all odd**. But *odd + odd = even*, so a+b would be **even** — contradicting a+b odd ✗

**Combining 7.1 and 7.2:** three cycles exist, and not all three are odd — so **at least one is even** ∎

> **Sanity check with numbers.** Say i=1, j=2, l=5. Then a=1, b=3, a+b=4. Lengths: 3, 5, **6** ← the third is even ✓
> Another: i=1, j=3, l=4. a=2, b=1, a+b=3. Lengths: **4**, 3, 5 ← the first is even ✓

**Where δ ≥ 3 was used:** we needed **three** neighbours to get three cycles. With only two neighbours (δ = 2) the argument dies — and rightly so: a triangle K₃ has δ = 2 and its only cycle is odd.

---

## 8. Trees

> A **tree** is a **connected, acyclic** graph. (Acyclic = contains no cycle.)

### Property 1 — a tree on n vertices has exactly n−1 edges

**First, a stepping stone:**

> **Every tree with n ≥ 2 vertices has a leaf** (a vertex of degree 1).

*Why:* a tree is connected, so no vertex has degree 0 (with n ≥ 2 that vertex would be cut off). If **every** vertex had degree ≥ 2, then δ ≥ 2, and **Lemma B** would hand us a cycle — but trees are acyclic. So some vertex has degree exactly 1. ✓

**Proof of Property 1, by induction on n.**

- **Base n = 1.** One vertex, no edges. 0 = 1 − 1 ✓
- **Step.** Let T be a tree on n ≥ 2 vertices. Grab a leaf **v** and delete it (along with its single edge), giving T′.
  - **T′ is still acyclic** — removing things can't create a cycle.
  - **T′ is still connected** — any path between two other vertices never passed *through* v (a degree-1 vertex has no way in and out; it can only be an endpoint).
  - So T′ is a tree on n−1 vertices → by induction it has **n−2** edges.
- Put v back: we restore 1 edge. T has (n−2) + 1 = **n−1** edges. ∎

### Property 2 — in a tree, the path between any two vertices is unique

*(My notes said "between any 2 edges" — should be **vertices**.)*

**Proof.** T is connected, so **at least one** path exists between any u and v. Suppose there were **two different** paths P and Q from u to v.

Walk along both from u simultaneously. They start together; since P ≠ Q they must **split apart** at some vertex — call the last shared vertex before the split **x**. After x they run separately; since both end at v, they must **meet again** — let **y** be the first vertex after x that lies on both.

```
        P-route
   x ●━━━━━━━━━━━━● y
     ┗━━━━━━━━━━━━┛
        Q-route
```

The two routes from x to y share **only** x and y (by how we picked them), and they're **different** routes. Glue them: **x → (P-route) → y → (Q-route backwards) → x** is a **cycle**.

But T is acyclic. **Contradiction.** So the path is unique. ∎

---

## 9. Bipartite Graphs

> A graph is **bipartite** if its vertices can be partitioned into **2 independent sets** X and Y — meaning every edge has one endpoint in X and the other in Y, and there are **no edges inside X or inside Y**.

```
   X:  ●   ●   ●
       |\ /|  /
       | X | /          every edge crosses the divide
       |/ \|/
   Y:  ●   ●
```

Think of it as **2-colouring** the vertices so that no edge joins two vertices of the same colour.

### Theorem — if G contains an **odd cycle**, then G is **not** bipartite

**Proof.** Suppose G were bipartite with parts X and Y, and let **v₁ v₂ … vₛ v₁** be a cycle of length s.

Every edge crosses between X and Y, so consecutive cycle vertices **alternate sides**. Say v₁ ∈ X. Then:

$$v_1 \in X,\; v_2 \in Y,\; v_3 \in X,\; v_4 \in Y, \dots$$

Pattern: **vₜ ∈ X exactly when t is odd.**

To *close* the cycle, the last vertex vₛ must be adjacent to v₁ ∈ X, which forces **vₛ ∈ Y**, i.e. **s is even**.

So in a bipartite graph **every** cycle is even. An odd cycle therefore rules out bipartiteness. ∎

### Theorem — if G is **not** bipartite, then G contains an odd cycle

Class noted this is best attacked through its **contrapositive**:

> **Contrapositive:** if G contains **no odd cycle**, then G **is** bipartite.

*(Reminder: "A ⇒ B" and "not B ⇒ not A" are logically identical statements. Proving one proves the other.)*

**Proof.** It's enough to handle one connected component at a time (colour each independently, then merge). So assume G is connected and has no odd cycle.

Pick any vertex **r** as a root. For each vertex v let **d(v)** = length of the shortest path from r to v. Now split by parity:

$$X = \{\,v : d(v) \text{ even}\,\}, \qquad Y = \{\,v : d(v) \text{ odd}\,\}.$$

We must show **no edge lies inside X, and none inside Y** — that's exactly what bipartite means.

Suppose an edge **uv** has both ends in the same part, so **d(u) and d(v) have the same parity**.

Take a shortest path from r to u and one from r to v. Let **w** be the **last vertex they share**. Then:

- the leg **w → u** has length d(u) − d(w)
- the leg **w → v** has length d(v) − d(w)
- these two legs share only **w** (by choice of w)

Now close a cycle: **w → u → v → back to w**, using the edge uv:

$$\text{length} = \big(d(u) - d(w)\big) \;+\; 1 \;+\; \big(d(v) - d(w)\big) = d(u) + d(v) - 2d(w) + 1.$$

Since d(u) and d(v) have the **same parity**, their sum **d(u) + d(v) is even**. Subtracting the even number 2d(w) keeps it even. Adding 1 makes it **odd**.

So we've produced an **odd cycle** — contradicting our assumption. Hence no such edge exists, and X, Y are independent sets. **G is bipartite.** ∎

### Summary

> **G is bipartite ⟺ G has no odd cycle.**

---

## 10. Takeaways

1. **"Many edges" is a global statement** — it can't control any individual vertex. Hunt for a *subgraph* instead (§4).
2. **Edge density = ½ × average degree.** Same fact, two costumes.
3. **Deleting a low-degree vertex raises the density** — that one observation drives the whole §4 theorem.
4. **Maximal beats longest.** "Can't be extended" is all these proofs need, and it's cheap to find (poly time vs NP-complete).
5. **The universal move:** take a maximal path, look at its endpoint, note that *all its neighbours are stuck on the path*, then count.
6. **Parity arguments** (§7, §9) — when you need "even", build several objects and use *odd + odd = even* to force one of them.
7. **Contrapositive** is often the easier door into a theorem (§9).

---

## Doubts / to revisit

- [ ] My notes wrote `|A| ≤ δ` for the long-path proof — should be **|A| ≥ δ**. (Corrected in [[2026-07-24 Long Path Theorem]].)
- [ ] Notes said "in a tree, path between any 2 **edges** is unique" — should be **vertices**.
- [ ] Diestel Ch. 1 — 23 problems (homework)
- [ ] Class flagged: "Wnt: Hamiltonian cycle proof technique" — revisit when we reach Hamiltonian graphs
