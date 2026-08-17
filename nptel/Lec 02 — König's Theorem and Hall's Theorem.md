---
tags: [academics, graph-theory, nptel, lecture]
lecture: 2
unit: Covering Problems
source: NPTEL Graph Theory (Dr. L. Sunil Chandran, IISc) — Lecture 02
---

# Lec 02 — Matchings: König's Theorem and Hall's Theorem

**◀ Previous:** [[Lec 01 — Vertex Cover and Independent Set]] · **Index:** [[NPTEL Index]] · **Next ▶** [[Lec 03 — More on Hall's Theorem and Applications]]

**Covered:** alternating and augmenting paths, Berge's theorem, König's min-max theorem for bipartite graphs, Hall's marriage theorem, and how the last two imply each other.

> These are my own worked-out write-ups of the mathematics, not a transcript. Where a proof can go several ways I give the cleanest standard route and flag alternatives.

---

## 0. Symbols used

| Symbol | Meaning |
|---|---|
| **G = (A ∪ B, E)** | bipartite graph with the two sides A and B; every edge joins A to B |
| **M** | a matching (set of pairwise disjoint edges) |
| **ν(G)** | maximum matching size |
| **τ(G)** | minimum vertex cover size |
| **N(S)** | the set of all neighbours of vertices in S |
| **M-saturated** | a vertex that is an endpoint of some edge of M ("matched") |
| **M △ M′** | symmetric difference — edges in exactly one of M, M′ |

> **Reminder from [[2026-07-24 Preliminaries]] §9:** *bipartite* means the vertices split into two independent sets. Equivalently, **no odd cycles**. That "no odd cycles" is the hidden engine of everything below.

---

## 1. Alternating and augmenting paths

Fix a matching M.

> An **M-alternating path** is a path whose edges alternate: **in M, not in M, in M, not in M, …**

> An **M-augmenting path** is an alternating path whose **two endpoints are both unmatched**.

```
 unmatched            unmatched
    u  ---- v ==== w ---- x        ---- = not in M
              (M)                  ==== = in M
```

### Why "augmenting" — the flip

An augmenting path starts and ends with **non-matching** edges, so along a path with 2k+1 edges it has **k+1** non-matching and **k** matching edges. **Swap them** — take the non-matching edges in, throw the matching edges out:

```
 before:  u ---- v ==== w ---- x        M-edges here: 1
 after:   u ==== v ---- w ==== x        M-edges here: 2   ← gained one!
```

The result is still a matching (the interior vertices each swap one partner for another; the two endpoints were unmatched so nothing clashes), and it has **one more edge**.

> **So: an augmenting path is a certificate that your matching is not maximum.** Berge's theorem says that's the *only* obstruction.

---

## 2. ★ Berge's Theorem

> **Theorem (Berge).** A matching M is **maximum** ⟺ there is **no M-augmenting path**.

**Proof.**

**(⇒) If M is maximum, no augmenting path exists.** Contrapositive: if an augmenting path existed, the flip above would produce a strictly larger matching, so M wasn't maximum ✓

**(⇐) If no augmenting path exists, M is maximum.** Contrapositive again: suppose M is *not* maximum, so some matching M′ has |M′| > |M|. Look at the **symmetric difference**

$$H := M \,\triangle\, M' \quad (\text{edges in exactly one of them}).$$

**Key structural fact:** every vertex touches **at most one** edge of M and **at most one** of M′, so in H every vertex has degree **≤ 2**. A graph with maximum degree 2 is a disjoint union of **paths and cycles**.

Moreover, along any of these paths or cycles the edges must **alternate** between M and M′ — two consecutive edges from the same matching would share a vertex, which matchings forbid.

Now count. Since |M′| > |M|, some component of H contains **more M′-edges than M-edges**. Which components can do that?

- A **cycle** alternates, so it's even and has **equally many** of each ✗
- A **path with an even number of edges** starts and ends with different types, again **equal** ✗
- A **path with an odd number of edges** — this one has one more of whichever type it starts and ends with.

So the surplus component is an odd path **beginning and ending with M′-edges**. Call it P.

Its two endpoints are unmatched by M: the end edge belongs to M′ and not M, and if the endpoint had an M-edge, that edge would continue the path in H. So **P is an M-augmenting path** ✓

Contradiction — we assumed none existed. Hence M is maximum ∎

> **Why this is the workhorse:** it converts "is my matching biggest?" into "can I find an augmenting path?", which is a **search** you can actually run. Every matching algorithm — Hopcroft–Karp, Hungarian, Edmonds' blossom — is built on hunting augmenting paths.

---

## 3. ★ König's Theorem

> **Theorem (König, 1931).** In a **bipartite** graph, $\nu(G) = \tau(G)$ — the maximum matching equals the minimum vertex cover.

We already know **ν ≤ τ** for every graph ([[Lec 01 — Vertex Cover and Independent Set]] §3). So the whole job is to build a vertex cover of size exactly ν.

### Proof (alternating reachability — the constructive route)

Let M be a **maximum** matching, and let

$$U := \{\text{vertices in } A \text{ not matched by } M\}.$$

Let **Z** be the set of all vertices reachable from U by **M-alternating paths** (paths starting at U, first edge not in M, then alternating). Split it:

$$S := Z \cap A, \qquad T := Z \cap B.$$

Note **U ⊆ S** (each u ∈ U reaches itself by the empty path).

**Claim: $K := (A \setminus S) \cup T$ is a vertex cover of size |M|.**

**(a) Every vertex of T is matched, and its partner lies in S.**
If some t ∈ T were unmatched, the alternating path from U to t would start and end unmatched — an **M-augmenting path**. By Berge that contradicts M being maximum ✗ So t is matched, say to a ∈ A. Extend the alternating path reaching t by the matching edge ta; that path is still alternating, so **a ∈ S** ✓

**(b) No edge joins S to B ∖ T.**
Suppose s ∈ S and b ∉ T with edge sb. Take the alternating path reaching s. Two cases, and both put b in T:
- if the path arrives at s along a **matching** edge (or s ∈ U, arriving along nothing), then appending the non-matching edge sb keeps it alternating → b ∈ T ✗
- s cannot be reached along a non-matching edge unless s ∈ U, since any alternating path entering A from B must do so along an M-edge (by (a)'s construction) ✓

So no such edge exists ✓

**(c) K is a vertex cover.**
Take any edge ab with a ∈ A, b ∈ B. If a ∉ S then a ∈ A ∖ S ⊆ K ✓ If a ∈ S then by (b) we must have b ∈ T ⊆ K ✓ Either way the edge is covered ✓

**(d) |K| ≤ |M|.**
Every vertex of **A ∖ S** is matched — the unmatched A-vertices are exactly U ⊆ S. Every vertex of **T** is matched, by (a). So each vertex of K sits on its own M-edge. Could two vertices of K share the same M-edge? That would need an M-edge from A ∖ S to T — but by (a) every T-vertex is matched **into S**, not into A ∖ S ✗ So the M-edges are distinct:

$$|K| \le |M| = \nu.$$

Therefore **τ ≤ |K| ≤ ν**, and with ν ≤ τ we conclude **ν = τ** ✓ ∎

**Worked check on the path a–b–c–d** (bipartite: A = {a, c}, B = {b, d}):

```
 a ——— b ——— c ——— d
```

ν = 2 (edges ab and cd), τ = 2 (cover {b, c}). Equal ✓

**And on K₃** (not bipartite): ν = 1, τ = 2. **Unequal** — showing bipartiteness is genuinely needed.

> **Alternative proofs, flagged.** König also follows (i) from **Hall's theorem** — see §5; (ii) from the **max-flow min-cut theorem** by making the bipartite graph a unit-capacity network (Lecture 31); (iii) from **Dilworth's theorem** (Lecture 08). All four are essentially the same theorem in different clothing.

---

## 4. ★ Hall's Theorem (the Marriage Theorem)

> **Theorem (Hall, 1935).** Let G be bipartite with sides A and B. There is a matching **saturating every vertex of A** ⟺
> $$|N(S)| \ge |S| \quad \text{for every } S \subseteq A.$$

The condition is called **Hall's condition**. In the marriage phrasing: A is a set of people, B the possible partners, edges are "would accept". Everyone in A can be married off iff **no group of k people collectively knows fewer than k candidates**.

### (⇒) Necessity — the easy direction

Suppose a matching saturates A, and take any S ⊆ A. Each vertex of S has its own partner, all in N(S), and the partners are **distinct** (it's a matching). So N(S) contains at least |S| vertices ✓

### (⇐) Sufficiency — induction on |A|

**Base |A| = 1.** Hall's condition on S = A gives |N(A)| ≥ 1, so the single vertex has a neighbour. Match them ✓

**Inductive step.** Assume the theorem for all smaller left-sides. Split on how *tight* Hall's condition is.

---

**Case 1 — slack everywhere: |N(S)| ≥ |S| + 1 for every non-empty proper S ⊊ A.**

Pick any vertex a ∈ A and any neighbour b (exists since |N({a})| ≥ 1). **Match a to b** and delete both.

Does Hall's condition survive in G − a − b? For any S ⊆ A ∖ {a}, deleting b removes at most one vertex from its neighbourhood:

$$|N_{G-a-b}(S)| \;\ge\; |N_G(S)| - 1 \;\ge\; (|S| + 1) - 1 \;=\; |S| \;✓$$

So by induction A ∖ {a} can be matched; add the edge ab ✓

---

**Case 2 — some tight set: |N(S)| = |S| for a non-empty proper S ⊊ A.**

The set S uses up its neighbourhood *exactly*. Handle it separately and then handle the rest.

**Step 1.** Hall's condition holds inside the subgraph on S ∪ N(S) (for T ⊆ S, N of T is the same there as in G). Since |S| < |A|, induction gives a matching saturating **S**, using up all of N(S).

**Step 2.** Let G′ be what remains: sides **A ∖ S** and **B ∖ N(S)**. Check Hall's condition there. Take T ⊆ A ∖ S. Apply Hall's condition in G to the union S ∪ T:

$$|N_G(S \cup T)| \;\ge\; |S| + |T|.$$

But $N_G(S \cup T) = N(S) \cup N_G(T)$, and |N(S)| = |S|, so the part of $N_G(T)$ **outside** N(S) must supply the remaining |T|:

$$|N_{G'}(T)| \;=\; |N_G(T) \setminus N(S)| \;\ge\; (|S| + |T|) - |S| \;=\; |T| \;✓$$

Since |A ∖ S| < |A|, induction matches A ∖ S inside G′.

**Step 3.** The two matchings use **disjoint** vertices (Step 1 lives in S ∪ N(S), Step 2 avoids both). Their union saturates A ✓ ∎

**A failure to look at.** A = {a₁, a₂, a₃}, B = {b₁, b₂}, with all three aᵢ joined to both bⱼ. Take S = A: |N(S)| = 2 < 3 = |S|. Hall fails, and indeed three people cannot be matched to two partners ✓

---

## 5. König ⟺ Hall

The two theorems are equivalent — each is a two-line consequence of the other.

### Hall ⇒ König

Let G be bipartite with sides A, B, and let K be a **minimum** vertex cover, so |K| = τ. Write

$$K_A := K \cap A, \qquad K_B := K \cap B.$$

Consider the bipartite subgraph H between $A \setminus K_A$ and $K_B$. Hall's condition holds in H: if some $S \subseteq A \setminus K_A$ had $|N_H(S)| < |S|$, we could swap $N_H(S)$ into the cover in place of S — replacing part of K by something strictly smaller and still covering everything — contradicting minimality of K.

So H has a matching saturating $A \setminus K_A$, and symmetrically one saturating $K_A$ on the other side. Assembling gives a matching of size |K| = τ, so ν ≥ τ. With ν ≤ τ, equality ✓

### König ⇒ Hall

Suppose Hall's condition holds. If no matching saturated A, then ν < |A|, so by König **τ = ν < |A|**. Take a minimum cover K, and set S := A ∖ K. All edges leaving S must be covered on the B-side, so

$$N(S) \subseteq K \cap B \quad\Longrightarrow\quad |N(S)| \le |K| - |K \cap A| = \tau - (|A| - |S|) < |A| - |A| + |S| = |S|,$$

violating Hall's condition ✗ So a saturating matching exists ✓

> **The moral:** König is the *min-max* form ("the largest packing equals the smallest cover") and Hall is the *feasibility* form ("here is exactly when a perfect assignment exists"). Min-max theorems and feasibility criteria are usually two faces of one result — a pattern you'll meet again with Menger (Lecture 10) and max-flow min-cut (Lecture 31).

---

## Takeaways

1. **Augmenting path = proof your matching isn't maximum.** Flip it and gain one edge.
2. **Berge's theorem** says that's the *only* obstruction — which turns optimality into a searchable condition, and underlies every matching algorithm.
3. The symmetric difference **M △ M′** always splits into alternating **paths and cycles** — max degree 2 is all you need for that. This trick reappears constantly.
4. **König:** in bipartite graphs ν = τ. The proof *constructs* the cover from alternating reachability out of the unmatched vertices.
5. **Hall:** matching all of A is possible iff no set of A-vertices is starved of neighbours. Proved by induction, splitting on whether some set is **tight**.
6. **The tight-set case is the heart of Hall's proof** — a set with |N(S)| = |S| can't spare any neighbours, so you must dispose of it first and recurse on what's left.
7. **König, Hall, Menger, max-flow min-cut and Dilworth are all the same theorem** in different disguises.

---

## Doubts / to revisit

- [ ] I proved König via alternating reachability. Chandran may instead derive it from Hall, or defer it to max-flow min-cut — worth checking which route the lecture takes.
- [ ] The Hall ⇒ König direction above is stated compactly; expand it if it's needed in full detail.
- [ ] Hopcroft–Karp running time O(E√V) — mentioned, not proved.
