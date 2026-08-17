---
tags: [academics, graph-theory, nptel, lecture]
lecture: 3
unit: Covering Problems
source: NPTEL Graph Theory (Dr. L. Sunil Chandran, IISc) — Lecture 03
---

# Lec 03 — More on Hall's Theorem and Some Applications

**◀ Previous:** [[Lec 02 — König's Theorem and Hall's Theorem]] · **Index:** [[NPTEL Index]] · **Next ▶** *(Lec 04 — Tutte's Theorem, not yet written)*

**Covered:** the defect version of Hall's theorem, regular bipartite graphs, decomposition into perfect matchings, systems of distinct representatives, Latin square extension, and Birkhoff–von Neumann.

> These are my own worked-out write-ups of the mathematics, not a transcript. Where a proof can go several ways I give the cleanest standard route and flag alternatives.

---

## 0. Symbols used

| Symbol | Meaning |
|---|---|
| **G = (A ∪ B, E)** | bipartite graph with sides A and B |
| **N(S)** | set of all neighbours of vertices in S |
| **ν(G)** | maximum matching size |
| **def(S)** | the **deficiency** \|S\| − \|N(S)\| of a set S ⊆ A |
| **k-regular** | every vertex has degree exactly k |
| **e(X, Y)** | number of edges between vertex sets X and Y |

---

## 1. ★ The Defect Version of Hall's Theorem

Hall's theorem answers *yes or no*. The defect version answers **"if not, how close did we get?"**

> **Theorem (Defect Hall / Ore).** For bipartite G with sides A and B,
> $$\nu(G) \;=\; |A| \;-\; \max_{S \subseteq A}\big(|S| - |N(S)|\big).$$

Write **def(S) := |S| − |N(S)|**. Since S = ∅ gives def(∅) = 0, the maximum is always ≥ 0. So the theorem says: **the number of A-vertices you must leave unmatched equals the worst deficiency of any set.**

> Ordinary Hall is the special case: max deficiency = 0 ⟺ ν = |A| ⟺ all of A is matched ✓

### Proof — by adding dummy vertices

**The trick.** Let **d := max over S of def(S)**. Hall fails only because some sets are starved of neighbours. So **feed them**: add d brand-new vertices to side B, each joined to **every** vertex of A. Call the enlarged graph G⁺.

**Step 1: Hall's condition now holds in G⁺.** For any S ⊆ A, if S is non-empty then all d new vertices are neighbours of S, so

$$|N_{G^+}(S)| = |N_G(S)| + d \;\ge\; |N_G(S)| + \big(|S| - |N_G(S)|\big) = |S| \;✓$$

(using d ≥ def(S) by definition of d).

**Step 2:** By **Hall's theorem** applied to G⁺, there's a matching M⁺ saturating all of A, so |M⁺| = |A|.

**Step 3: delete the dummies.** At most **d** edges of M⁺ use a new vertex (there are only d of them, and a matching uses each at most once). Removing those leaves a genuine matching in G of size

$$\ge |A| - d \quad\Longrightarrow\quad \nu(G) \ge |A| - d.$$

**Step 4: the reverse inequality.** Take S achieving the maximum, so |N(S)| = |S| − d. Any matching can match the vertices of S only into N(S), so at most |N(S)| = |S| − d of them get matched, leaving **at least d** vertices of S unmatched. Hence

$$\nu(G) \le |A| - d.$$

Both directions give **ν(G) = |A| − d** ✓ ∎

**Worked example.** A = {a₁, a₂, a₃, a₄}, B = {b₁, b₂}, with a₁, a₂, a₃ all joined only to b₁ and b₂, and a₄ joined to b₂.

Take S = {a₁, a₂, a₃}: N(S) = {b₁, b₂}, so def(S) = 3 − 2 = **1**. Taking S = A gives def = 4 − 2 = **2**, which is the max. So ν = 4 − 2 = **2** ✓ (Indeed only two edges can be disjoint — B has just two vertices.)

---

## 2. ★ Every k-regular bipartite graph has a perfect matching

> **Theorem.** If G is bipartite and **k-regular** with k ≥ 1, then G has a **perfect matching**.

### First: the two sides are equal

Count the edges **twice**, once from each side. Every edge has exactly one end in A and one in B, and every vertex has degree k:

$$|E| = k|A| \quad\text{and}\quad |E| = k|B| \quad\Longrightarrow\quad k|A| = k|B| \quad\Longrightarrow\quad |A| = |B|$$

(dividing by k ≥ 1) ✓ So a matching saturating A is automatically **perfect**.

### Now verify Hall's condition

Take any S ⊆ A and count the edges leaving S, again two ways.

- **From the S side:** every vertex of S has degree exactly k, so $e(S, N(S)) = k|S|$.
- **From the N(S) side:** every edge out of S lands in N(S). Each vertex of N(S) has degree k in total — some of those edges may go to A ∖ S — so N(S) can absorb **at most** k|N(S)| edges:

$$e(S, N(S)) \;\le\; k\,|N(S)|.$$

```
     S            N(S)
     ●━━━━━━━━━━━━●          every edge from S lands in N(S),
     ●━━━━━━━━━━━━●          but N(S) may also receive edges
     ●━━━━━━━━━━━━●   ◀━━━●  from outside S
```

Putting them together:

$$k|S| \;=\; e(S, N(S)) \;\le\; k|N(S)| \quad\Longrightarrow\quad |N(S)| \ge |S| \;✓$$

Hall's condition holds, so a matching saturating A exists — and since |A| = |B|, it is **perfect** ✓ ∎

> **The pattern to remember:** *count one quantity two ways, then compare.* Regularity makes the count from S exact and the count into N(S) an inequality — and the gap between "exact" and "at most" is precisely Hall's condition.

---

## 3. ★ k-regular bipartite graphs split into k perfect matchings

> **Theorem (König's edge-colouring theorem, regular case).** The edge set of a k-regular bipartite graph decomposes into exactly **k disjoint perfect matchings**.

**Proof by induction on k.**

- **Base k = 1.** A 1-regular graph *is* a perfect matching ✓
- **Step.** Let G be k-regular bipartite with k ≥ 2. By §2 it has a perfect matching M. Remove M's edges. Every vertex loses exactly one edge (M is perfect, so it touches each vertex once), leaving a **(k−1)-regular** bipartite graph. By induction that decomposes into k−1 perfect matchings; together with M that's **k** ✓ ∎

**Consequence:** the **edge chromatic number** of a k-regular bipartite graph is exactly k — colour each perfect matching with its own colour. This is the bipartite case of Vizing's theorem territory (Lectures 15–16), where in general you may need Δ+1 colours. **Bipartite graphs never need the extra colour.**

**Example — K₃,₃** is 3-regular bipartite, so it splits into 3 perfect matchings:

```
 a₁ a₂ a₃      matching 1:  a₁b₁  a₂b₂  a₃b₃
  |╲ |╱ |      matching 2:  a₁b₂  a₂b₃  a₃b₁
  | ╳  ╲|      matching 3:  a₁b₃  a₂b₁  a₃b₂
 b₁ b₂ b₃      → all 9 edges used exactly once ✓
```

---

## 4. Systems of Distinct Representatives (SDRs)

> Given finite sets **S₁, S₂, …, Sₙ**, a **system of distinct representatives** is a choice of one element xᵢ ∈ Sᵢ for each i, with all the xᵢ **distinct**.

> **Theorem.** An SDR exists ⟺ for every index set I ⊆ {1,…,n},
> $$\Big|\bigcup_{i \in I} S_i\Big| \;\ge\; |I|.$$

**Proof — it's Hall's theorem in different clothing.** Build a bipartite graph:

- side **A** = the indices {1, …, n}
- side **B** = all elements appearing in any Sᵢ
- join index i to element x whenever **x ∈ Sᵢ**

Then N({i}) = Sᵢ, and more generally **N(I) = ⋃_{i∈I} Sᵢ**. An SDR is exactly a matching saturating A. Hall's condition |N(I)| ≥ |I| translates verbatim into the union condition ✓ ∎

**Example.** S₁ = {1,2}, S₂ = {1,2}, S₃ = {1,2}. Taking I = {1,2,3}: the union is {1,2}, size 2 < 3 ✗ **No SDR** — three sets fighting over two elements.

**Example.** S₁ = {1,2}, S₂ = {2,3}, S₃ = {1,3}. Every union of k sets has ≥ k elements ✓ SDR exists: pick 1, 2, 3 ✓

---

## 5. Extending a Latin rectangle to a Latin square

> An **r × n Latin rectangle** is an r-row, n-column array filled with symbols 1…n so that **no symbol repeats in any row or any column**.
> A **Latin square** is the case r = n.

> **Theorem.** Every r × n Latin rectangle with **r < n** can be extended by one more row — and hence, repeating, to a full **n × n Latin square**.

**Proof.** We must fill row r+1. Build a bipartite graph:

- side **A** = the n **columns**
- side **B** = the n **symbols**
- join column c to symbol s if **s does not yet appear in column c**

A valid new row is exactly a **perfect matching**: each column gets one symbol, no symbol used twice, and no clash within a column.

**Claim: this graph is (n − r)-regular**, hence has a perfect matching by §2.

- **Degree of a column c.** Column c currently holds r entries, all distinct (no repeats in a column), so exactly **n − r** symbols are still available → degree n − r ✓
- **Degree of a symbol s.** Symbol s appears exactly **once in each of the r rows** (each row is a permutation of all n symbols), and those r occurrences lie in **r different columns** — two occurrences in the same column would repeat within that column ✗ So s is missing from exactly **n − r** columns → degree n − r ✓

Both sides are (n−r)-regular, so §2 gives a perfect matching, which is a legal new row ✓

Repeat until r = n ✓ ∎

**Worked example.** n = 3, and the 1 × 3 rectangle `1 2 3`.

Available symbols per column: col 1 → {2,3}, col 2 → {1,3}, col 3 → {1,2} — each of degree 2 = n − r ✓
A perfect matching: col 1 → 2, col 2 → 3, col 3 → 1, giving row 2 = `2 3 1` ✓ Then row 3 = `3 1 2` ✓

```
 1 2 3
 2 3 1     a Latin square
 3 1 2
```

---

## 6. Birkhoff–von Neumann (a flagged application)

> A **doubly stochastic matrix** is a square matrix of non-negative reals whose every row and every column sums to **1**.

> **Theorem (Birkhoff–von Neumann).** Every doubly stochastic matrix is a **convex combination of permutation matrices**.

**Sketch of why Hall gives this.** Given a doubly stochastic matrix P, build a bipartite graph joining row i to column j whenever **Pᵢⱼ > 0**. Hall's condition holds — a set S of rows carries total mass |S| (each row sums to 1), and all of it lands in the columns of N(S), which can hold at most |N(S)| in total, so |N(S)| ≥ |S| ✓

So there's a perfect matching, i.e. a **permutation** σ with every P(i, σ(i)) > 0. Subtract the largest possible multiple of that permutation matrix; this zeroes out at least one entry while keeping the matrix doubly stochastic (after rescaling). Induct on the number of non-zero entries ✓

> Flagged as a sketch rather than a full proof — the induction bookkeeping is fiddly and it's usually stated as an application rather than proved in detail at this point in a course.

---

## Takeaways

1. **Defect Hall** converts a yes/no criterion into a formula: the number of unmatched vertices equals the **worst deficiency**. The proof trick is to **add dummy vertices** to repair Hall's condition, then delete them and count the damage.
2. **Regularity ⇒ Hall's condition**, by counting edges out of S two ways. This is the single most reused argument in the lecture.
3. **k-regular bipartite ⇒ k disjoint perfect matchings.** Peel one off, the rest stays regular, recurse.
4. Bipartite graphs are **edge-colourable in exactly Δ colours** — no extra colour needed, unlike the general case.
5. **SDRs are Hall's theorem relabelled** — indices on one side, elements on the other.
6. **Latin rectangles extend** because "which symbols are still free" forms an (n−r)-regular bipartite graph — the regularity does all the work.
7. The recurring shape: *set up a bipartite graph where the thing you want is a perfect matching, then verify Hall (usually via regularity).* Almost every application in this lecture follows that template.

---

## Doubts / to revisit

- [ ] Chandran may prove defect Hall directly by induction rather than by the dummy-vertex trick — worth comparing.
- [ ] Birkhoff–von Neumann is only sketched here; ask whether the full proof is examinable.
- [ ] Is the Latin square extension result examinable, or just an illustration?
