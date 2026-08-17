---
tags: [academics, graph-theory, lecture]
date: 2026-08-10
seq: 7
class: 5
---

# 7 · 2026-08-10 — Matchings in Bipartite Graphs

**◀ Previous:** [[Tutorial 1]]  ·  **Hub:** [[Graph Theory]]  ·  **Next ▶** *(none yet — latest note)*

**Covered:** perfect matchings, the question of whether some vertex must lie in *every* maximum matching, why that fails for odd cycles, and the theorem that it always holds in **bipartite** graphs.

---

## 0. Symbols used today

| Symbol | Meaning |
|---|---|
| **M, N** | matchings |
| **V(M)** | the set of vertices **matched** by M |
| **H = M ∪ N** | the union of two matchings, viewed as a graph on all of V(G) |
| **M △ P** | symmetric difference — written in class as **M∖P + P∖M** |
| **\|MVC\|** | size of a minimum vertex cover *(standard: τ)* |
| **perfect matching** | see below |

---

## 1. Perfect matchings

> A **perfect matching** is a matching of size **n/2** — every vertex is matched.

Equivalently: **V(M) = V(G)**, nothing left over. A perfect matching only exists when n is even.

**Examples from class:**

| Graph | Maximum matching | Perfect? |
|---|---|---|
| **K₂ₙ** | n | ✅ yes |
| **C₂ₙ** (even cycle) | n | ✅ yes |
| **C₂ₙ₊₁** (odd cycle) | n | ❌ one vertex always left out |
| Path a–b–c–d–e | 2 | ❌ n is odd |

For the 5-path the maximum matchings are {ab, cd}, {ab, de}, {bc, de} — each leaves exactly one vertex unmatched.

---

## 2. The question: must some vertex be in *every* maximum matching?

> **Question.** Does there always exist a vertex that belongs to **every** maximum matching?

### ❌ No — odd cycles are the counterexample

Take **C₂ₙ₊₁**. Every maximum matching has n edges and therefore misses **exactly one** vertex. But the odd cycle is **vertex-transitive** — it looks identical from every vertex — so for *any* vertex v you can rotate a maximum matching until v is the one left out.

```
   C₅:   a — b        {ab, cd} misses e
        /     \       {bc, de} misses a
       e       c      {cd, ea} misses b   … and so on
        \     /
         d — —        → every vertex is missed by some maximum matching
```

So **no vertex lies in all of them** ✗

### ✅ Yes for trees

> **In a tree, the parent of a leaf lies in every maximum matching.**

**Why.** Let u be a leaf with neighbour (parent) v, and let M be any maximum matching. If v were unmatched, then u would be unmatched too — u's only possible partner is v — and **M + uv** would be a strictly bigger matching ✗ contradicting maximality. So v ∈ V(M) ✓

> Compare with [[2026-07-29 Matchings 2 — Berge and König]] §2: there we showed the *edge* uv lies in **some** maximum matching. Here we get the stronger statement that the *vertex* v lies in **every** one. Different claims — note the some/every and edge/vertex swaps.

---

## 3. ★ Theorem — every bipartite graph has such a vertex

> **Theorem.** Let G be a **bipartite** graph with at least one edge. Then there exists a vertex that belongs to **every** maximum matching of G.

**Proof by contradiction.** Suppose not — so **for every vertex v there is a maximum matching that misses v**.

### Setting up

Pick any vertex **u**. By our assumption there is a maximum matching **M** with **u ∉ V(M)**. Let **x** be any neighbour of u.

**Claim 3.1 — x is matched by M.**
If x ∉ V(M) too, then neither endpoint of the edge ux is used, so **M + ux** is a strictly larger matching ✗ contradicting that M is maximum. Hence **x ∈ V(M)** ✓

By our assumption again, there is a maximum matching **N** with **x ∉ V(N)**.

Now form the union

$$H \;:=\; M \cup N .$$

### Claim 3.2 — what H looks like

Every vertex meets **at most one** M-edge and **at most one** N-edge, so **Δ(H) ≤ 2**. A graph of maximum degree ≤ 2 is a disjoint union of **paths and cycles**, and along each the edges must **alternate** between M and N (two adjacent edges from the same matching would share a vertex ✗).

Moreover **|M| = |N|**, since both are maximum. So no component can carry a surplus of either — which rules out odd-length alternating paths. Every component of H is therefore:

- an **isolated vertex**, or
- a **single edge lying in both M and N**, or
- an **even-length path**, or
- an **even cycle** ✓

*(An odd-length alternating path would be augmenting for whichever matching supplies its two end edges, contradicting that both M and N are maximum. That's the "no odd length paths ≥ 3" line in my notes.)*

### Claim 3.3 — u and x each have degree 1 in H

- **u** is missed by M but matched by N (N is maximum; if N missed u too then N + ux would be bigger ✗ by the same argument as Claim 3.1). So u meets exactly **one** edge of H — its N-edge ✓
- **x** is matched by M (Claim 3.1) but missed by N. So x meets exactly **one** edge of H — its M-edge ✓

Degree 1 means each is an **endpoint of a path component** of H. Let **P** be the path component having **u** as an endpoint. By Claim 3.2, **P has even length**, and the edge of P at u belongs to **N**.

### Claim 3.4 — swapping along P keeps both matchings maximum

Define

$$M' := M \,\triangle\, P, \qquad N' := N \,\triangle\, P .$$

P is an **even-length** alternating path, so it contains **equally many** M-edges and N-edges. Swapping therefore changes neither size:

$$|M'| = |M|, \qquad |N'| = |N| \quad\Longrightarrow\quad \text{both are still \textbf{maximum} matchings} \;✓$$

**And u is now unmatched by N′:** the single edge at u belonged to N and lay on P, so the swap removes it. Hence **u ∉ V(N′)** ✓

### The two cases

Everything now turns on whether x survives in N′.

**Case 1 — x ∉ V(N′).**

Then **both** u and x are unmatched by N′, and **ux is an edge of G**. So N′ + ux is a strictly larger matching ✗ contradicting that N′ is maximum (Claim 3.4) ✓

**Case 2 — x ∈ V(N′).**

Originally **x ∉ V(N)**, and the *only* edges whose membership changed were those on **P**. So x must have gained its edge from P, giving **x ∈ V(P)**.

But by Claim 3.3, x has **degree 1** in H — so x is an **endpoint** of P. A path has exactly two endpoints, and one of them is u. Therefore

> **P is a path from u to x, of even length.**

Now add the edge **ux** (which exists in G). Closing an even-length path with one more edge gives a cycle of length

$$\underbrace{|P|}_{\text{even}} + 1 \;=\; \textbf{odd}.$$

An **odd cycle** in G ✗ — but **G is bipartite**, and bipartite graphs have no odd cycles ([[2026-07-24 Preliminaries]] §9) ✓

### Combining

| | outcome |
|---|---|
| **Case 1** | a bigger matching than the maximum N′ ✗ |
| **Case 2** | an odd cycle in a bipartite graph ✗ |

Both cases are impossible, so the assumption was false. **Some vertex lies in every maximum matching** ∎

> ★ **Where bipartiteness is used: exactly once, in Case 2.** Everything up to that point is true for any graph. The odd cycle is the only thing that breaks — which is precisely why **C₂ₙ₊₁** is the counterexample in §2. The theorem is really saying: *odd cycles are the sole obstruction.*

---

## 4. Exercise — at least |MVC| such vertices

> **Exercise.** Let G be bipartite and let **k = |MVC(G)|**. Prove that at least **k** vertices of G belong to every maximum matching.

*(Set in class; here's a proof.)*

**Set-up.** By **König** ([[2026-07-29 Matchings 2 — Berge and König]] §6), bipartite graphs satisfy

$$|MM(G)| \;=\; |MVC(G)| \;=\; k,$$

so every maximum matching has exactly k edges.

**Proof by induction on k.**

**Base k = 0.** No edges, nothing to prove — zero vertices required ✓

**Inductive step.** Let k ≥ 1. By the **Theorem of §3**, there is a vertex **v** lying in every maximum matching. Put **G′ := G − v**.

**Claim 4.1 — |MM(G′)| = k − 1.**

- *(≤)* If G′ had a matching of size k, that same matching would be a maximum matching of G avoiding v ✗ contradicting the choice of v. So |MM(G′)| ≤ k−1.
- *(≥)* Take any maximum matching M of G. It contains an edge at v; delete that edge. The remaining k−1 edges avoid v, so they form a matching of G′ ✓

Hence |MM(G′)| = k−1, and since G′ is still **bipartite**, König gives **|MVC(G′)| = k−1** ✓

**Claim 4.2 — apply the induction hypothesis.**
G′ is bipartite with minimum vertex cover k−1, so by induction it has **at least k−1 vertices** lying in every maximum matching of G′ ✓

**Claim 4.3 — those vertices also lie in every maximum matching of G.**
Let M be any maximum matching of G, and let M⁻ be M with v's edge removed. By Claim 4.1, M⁻ is a matching of G′ of size k−1 = |MM(G′)| — so M⁻ is a **maximum matching of G′**.

Any vertex w from Claim 4.2 therefore satisfies w ∈ V(M⁻) ⊆ V(M) ✓

**Combining.** The k−1 vertices from Claim 4.2 all live in G′, so none of them is v. Adding v itself:

$$\ge (k-1) + 1 \;=\; k \quad\text{vertices lie in every maximum matching of } G \qquad \blacksquare$$

**Check.** The path a–b–c has k = |MVC| = 1 (cover {b}); its maximum matchings are {ab} and {bc}, and **b** is in both — exactly 1 ✓
The path a–b–c–d has k = 2 (cover {b,c}); its only maximum matching is {ab, cd}, so **all four** vertices qualify — comfortably ≥ 2 ✓

---

## Takeaways

1. **Perfect matching** = every vertex matched, size n/2.
2. **Odd cycles have no universal vertex** — vertex-transitivity means every vertex is missed by some maximum matching.
3. **In a tree, a leaf's parent is in every maximum matching** — otherwise the leaf could be added.
4. ★ **Every bipartite graph has a vertex in every maximum matching**, and the proof shows odd cycles are the *only* obstruction.
5. **M ∪ N with both maximum** ⇒ all components are even paths, even cycles, shared single edges, or isolated vertices. This decomposition keeps reappearing — see [[2026-07-29 Matchings 2 — Berge and König]] Claim 2.2.
6. **Swapping along an *even* alternating path preserves matching size** (whereas swapping along an *odd* one gains an edge — that's Berge). Knowing which parity does what is the whole trick.
7. **Bipartite + König ⇒ at least |MVC| universal vertices**, by peeling one off and inducting.

---

## Doubts / to revisit

- [ ] The §3 theorem needs G to have at least one edge — an edgeless graph has the empty matching as its unique maximum, and no vertex is in it. Worth checking whether the lecture stated that hypothesis.
- [ ] Is the bound in §4 tight? The path a–b–c achieves exactly k = 1; a–b–c–d exceeds it. Worth asking which graphs attain equality.
- [ ] Contrast carefully with [[2026-07-29 Matchings 2 — Berge and König]] §2: *the edge* uv is in **some** maximum matching (any graph) vs *the vertex* v is in **every** maximum matching (trees, bipartite).
