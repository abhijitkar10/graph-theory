---
tags: [academics, graph-theory, nptel, lecture]
lecture: 3
unit: Covering Problems
source: NPTEL Graph Theory (Dr. L. Sunil Chandran, IISc), Lecture 03
---

# Lec 03 — More on Hall's theorem, and some applications

Previous: [[Lec 02 — König's Theorem and Hall's Theorem]] · Index: [[NPTEL Index]] · Next: Lec 04 on Tutte's theorem, not yet written

Covered here: the defect version of Hall's theorem, regular bipartite graphs, decomposition into perfect matchings, systems of distinct representatives, Latin rectangle extension, and Birkhoff and von Neumann.

These are my own written up versions of the mathematics rather than a transcript. Where a proof can go several ways I give the cleanest standard route and mention the alternatives.

## How much this matters

Overall this note is useful, and one section of it is core.

Know cold: [[Lec 03 — More on Hall's Theorem and Applications#Every k regular bipartite graph has a perfect matching|the regularity argument]]. Counting the edges out of a set in two directions is the single most reused argument in the whole matchings unit, and the proof is four lines.

Know the trick: [[Lec 03 — More on Hall's Theorem and Applications#The defect version of Hall's theorem|defect Hall]], specifically the padding with dummy vertices and then subtracting them off.

Know the statement: [[Lec 03 — More on Hall's Theorem and Applications#k regular bipartite graphs split into k perfect matchings|the decomposition into k perfect matchings]] and its consequence for edge colouring.

Read once: [[Lec 03 — More on Hall's Theorem and Applications#Systems of distinct representatives|SDRs]], [[Lec 03 — More on Hall's Theorem and Applications#Extending a Latin rectangle to a Latin square|Latin rectangles]] and [[Lec 03 — More on Hall's Theorem and Applications#Birkhoff and von Neumann|Birkhoff and von Neumann]]. Good illustrations of one template, but none of them is on the class syllabus.

## Notation

G = (A ∪ B, E) is a bipartite graph with sides A and B. N(S) is the set of all vertices adjacent to something in S, and α′(G) is the matching number. The deficiency of a set S inside A is the size of S minus the size of N(S). A graph is k regular when every degree is exactly k, and e(X, Y) counts the edges between two vertex sets.

## The defect version of Hall's theorem

Hall's theorem answers yes or no. The defect version answers the follow up question, which is how close you got when the answer was no.

Theorem (defect Hall, Ore). For a bipartite graph G with sides A and B, the matching number α′(G) equals the size of A minus the largest deficiency over all subsets of A.

Since the empty set has deficiency zero, that largest deficiency is always at least zero. So the theorem says the number of A vertices you are forced to leave unmatched is exactly the worst deficiency of any set. Ordinary Hall is the special case where the largest deficiency is zero, which happens exactly when all of A can be matched.

### The proof, by adding dummy vertices

Let d be the largest deficiency. Hall fails only because some sets are starved of neighbours, so feed them. Add d brand new vertices to side B, each joined to every vertex of A, and call the enlarged graph G⁺.

First, Hall's condition holds in G⁺. For any non empty subset S of A, all d new vertices are neighbours of S, so its neighbourhood grows by exactly d. Since d is at least the deficiency of S by definition, the enlarged neighbourhood has at least the size of S.

Second, Hall's theorem applied to G⁺ gives a matching saturating all of A, so that matching has as many edges as A has vertices.

Third, delete the dummies. At most d edges of that matching use a new vertex, since there are only d new vertices and a matching uses each at most once. Removing those leaves a genuine matching in the original G of size at least the size of A minus d, so α′(G) ≥ |A| − d.

Fourth, the reverse inequality. Take a set S achieving the largest deficiency, so its neighbourhood has size exactly |S| − d. Any matching can match the vertices of S only into N(S), so at most |S| − d of them get matched, leaving at least d vertices of S unmatched. Hence α′(G) ≤ |A| − d.

Both directions together give equality.

A worked example. Let A have four vertices a₁, a₂, a₃, a₄ and B have two vertices b₁, b₂, with a₁, a₂ and a₃ all joined to both of them and a₄ joined only to b₂. Taking S to be {a₁, a₂, a₃} gives a neighbourhood of size 2 and a deficiency of 1. Taking S to be all of A gives a deficiency of 2, which is the largest. So α′ = 4 − 2 = 2, and indeed only two edges can be disjoint, since B has just two vertices.

## Every k regular bipartite graph has a perfect matching

Theorem. If G is bipartite and k regular with k at least 1, then G has a perfect matching.

Given: G is bipartite and k regular.
To show: some matching covers every vertex.

First, the two sides have equal size. Count the edges twice, once from each side. Every edge has exactly one end in A and one in B, and every vertex has degree k, so the edge count is both k times the size of A and k times the size of B. Dividing by k gives equal sides, and therefore a matching saturating A is automatically perfect.

Now verify Hall's condition. Take any subset S of A and count the edges leaving S in two directions.

From the S side the count is exact. Every vertex of S has degree exactly k and all of its edges leave S, since S sits inside A and edges only go to B, so exactly k times the size of S edges leave.

From the N(S) side the count is an inequality. Every edge out of S lands in N(S), and each vertex of N(S) has degree k in total, some of which may go to vertices of A outside S, so N(S) can absorb at most k times its own size.

```
     S            N(S)
     ●━━━━━━━━━━━━●          every edge from S lands in N(S),
     ●━━━━━━━━━━━━●          but N(S) may also receive edges
     ●━━━━━━━━━━━━●   ◀━━━●  from outside S
```

Comparing the two, k times the size of S is at most k times the size of N(S), so N(S) is at least as large as S, which is Hall's condition. Hall then gives a matching saturating A, and since the sides are equal that matching is perfect.

The pattern to remember is to count one quantity two ways and then compare. Regularity makes the count from S exact and the count into N(S) an inequality, and the gap between exact and at most is precisely Hall's condition.

## k regular bipartite graphs split into k perfect matchings

Theorem (König's edge colouring theorem, regular case). The edge set of a k regular bipartite graph decomposes into exactly k disjoint perfect matchings.

Induct on k. For the base case, a 1 regular graph is itself a perfect matching. For the step, let G be k regular bipartite with k at least 2. By the previous section it has a perfect matching M. Remove the edges of M, and every vertex loses exactly one edge since M is perfect and touches each vertex once, leaving a (k−1) regular bipartite graph. By induction that decomposes into k−1 perfect matchings, and together with M that makes k.

The consequence is that the edge chromatic number of a k regular bipartite graph is exactly k, by colouring each perfect matching with its own colour. This is the bipartite corner of Vizing's theorem, covered in Lectures 15 and 16, where a general graph may need Δ+1 colours. Bipartite graphs never need that extra colour.

For an example, K₃,₃ is 3 regular bipartite, so it splits into three perfect matchings.

```
 a₁ a₂ a₃      matching 1:  a₁b₁  a₂b₂  a₃b₃
  |╲ |╱ |      matching 2:  a₁b₂  a₂b₃  a₃b₁
  | ╳  ╲|      matching 3:  a₁b₃  a₂b₁  a₃b₂
 b₁ b₂ b₃      all nine edges used exactly once
```

## Systems of distinct representatives

Given finite sets S₁, S₂, …, Sₙ, a system of distinct representatives is a choice of one element from each set, with all the chosen elements distinct.

Theorem. Such a system exists exactly when, for every collection of indices, the union of the corresponding sets is at least as large as the number of indices.

This is Hall's theorem in different clothing. Build a bipartite graph whose left side is the indices, whose right side is all the elements appearing in any of the sets, and where index i is joined to element x whenever x lies in Sᵢ. Then the neighbourhood of a single index is its set, and the neighbourhood of a collection of indices is the union of their sets. A system of distinct representatives is exactly a matching saturating the left side, and Hall's condition translates verbatim into the union condition.

Two examples. With S₁ = S₂ = S₃ = {1, 2}, taking all three indices gives a union of size 2 against 3 indices, so no system exists, since three sets are fighting over two elements. With S₁ = {1,2}, S₂ = {2,3} and S₃ = {1,3}, every union of k sets has at least k elements, and a system exists by picking 1, 2 and 3.

## Extending a Latin rectangle to a Latin square

An r by n Latin rectangle is an array with r rows and n columns filled with the symbols 1 to n so that no symbol repeats in any row or any column. A Latin square is the case where r equals n.

Theorem. Every r by n Latin rectangle with r below n can be extended by one more row, and hence, repeating, to a full n by n Latin square.

We must fill row r+1. Build a bipartite graph whose left side is the n columns, whose right side is the n symbols, and where column c is joined to symbol s when s does not yet appear in column c. A valid new row is exactly a perfect matching, since each column gets one symbol, no symbol is used twice, and no clash arises within a column.

The claim is that this graph is (n−r) regular, which by the earlier section gives it a perfect matching.

For the degree of a column, that column currently holds r entries, all distinct since a column has no repeats, so exactly n − r symbols are still available to it.

For the degree of a symbol, that symbol appears exactly once in each of the r rows, since every row is a permutation of all n symbols, and those r occurrences lie in r different columns, because two occurrences in the same column would repeat within it. So the symbol is missing from exactly n − r columns.

Both sides are therefore (n−r) regular, which gives a perfect matching and so a legal new row. Repeat until r reaches n.

A worked example with n = 3, starting from the single row 1 2 3. The available symbols are {2,3} for column 1, {1,3} for column 2 and {1,2} for column 3, each of degree 2, which is n − r. One perfect matching sends column 1 to symbol 2, column 2 to 3 and column 3 to 1, giving the second row 2 3 1, and then the third row is 3 1 2.

```
 1 2 3
 2 3 1     a Latin square
 3 1 2
```

## Birkhoff and von Neumann

A doubly stochastic matrix is a square matrix of non negative reals in which every row and every column sums to 1.

Theorem (Birkhoff and von Neumann). Every doubly stochastic matrix is a convex combination of permutation matrices.

Here is why Hall gives this. Given a doubly stochastic matrix P, build a bipartite graph joining row i to column j whenever the entry at (i,j) is positive. Hall's condition holds, because a set S of rows carries a total mass equal to its size, since each row sums to 1, and all of that mass lands in the columns of N(S), which can hold at most the size of N(S) in total. So N(S) is at least as large as S.

That gives a perfect matching, which is a permutation with every corresponding entry positive. Subtract the largest possible multiple of that permutation matrix, which zeroes out at least one entry while keeping the matrix doubly stochastic after rescaling, and induct on the number of non zero entries.

This is a sketch rather than a full proof. The induction bookkeeping is fiddly, and the result is usually stated as an application rather than proved in detail at this point in a course.

## What to remember

Defect Hall converts a yes or no criterion into a formula, since the number of unmatched vertices equals the worst deficiency, and the proof trick is to add dummy vertices to repair Hall's condition and then delete them and count the damage. Regularity gives Hall's condition by counting the edges out of a set two ways, which is the single most reused argument in the lecture. A k regular bipartite graph splits into k disjoint perfect matchings, by peeling one off and recursing on what stays regular, and the consequence is that bipartite graphs are edge colourable in exactly Δ colours with no extra colour needed. Systems of distinct representatives are Hall relabelled, with indices on one side and elements on the other. Latin rectangles extend because the still free symbols form an (n−r) regular bipartite graph, and the regularity does all the work. The recurring shape of the whole lecture is to set up a bipartite graph in which the thing you want is a perfect matching, then verify Hall, usually via regularity.

## Still unclear

- Chandran may prove defect Hall directly by induction rather than by the dummy vertex trick. Worth comparing.
- Birkhoff and von Neumann is only sketched here. Worth asking whether the full proof is examinable.
- Whether the Latin square extension result is examinable or just an illustration.
