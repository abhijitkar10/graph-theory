---
tags: [academics, graph-theory, revision]
type: takeaways
---

# Takeaways, the distillation

Hub: [[Graph Theory]] · Full sheet: [[Revision Sheet]] · Depth: [[Master Notes]] · Shortest version: [[Bare Minimum]]

Statements only, no proofs. Eighty one of them, readable in twenty minutes.

## Language

1. Length means the number of edges, so a path on m vertices has length m−1.
2. A walk repeats anything, a trail repeats no edge, a path repeats no vertex, and a circuit is a closed trail.
3. Maximal means it cannot be extended. Maximum means none bigger exists anywhere. Maximal is cheap to find and maximum is NP complete, and every proof in these notes only needs maximal.
4. In an induced subgraph you pick the vertices and the edges are then forced. An induced path has no chords.
5. An empty graph means no edges, not no vertices.
6. α is independence, β is vertex cover, α′ is matching, β′ is edge cover. Unprimed refers to vertices and primed to edges, α means maximise and β means minimise.

## Numbers

7. The two Gallai identities are α + β = n and α′ + β′ = n. Primes pair with primes.
8. The sandwich α′ ≤ β ≤ 2α′ holds always. The lower end is tight for bipartite graphs and the upper end at the triangle.
9. Always α′ ≤ ⌊n/2⌋.
10. Paths, cycles and complete graphs all have α′ = ⌊n/2⌋. The exceptions are the star, with α′ = 1, and complete bipartite, with α′ = min(k,l).
11. Equality α′ = β holds exactly for the bipartite ones, and that pattern is König.
12. The hypercube Qₙ has 2ⁿ vertices, is n regular, has n·2ⁿ⁻¹ edges, diameter n, girth 4, a Hamiltonian cycle, and is bipartite. Q₄ is not planar.
13. Always κ ≤ λ ≤ δ.

## The extremal method, the one technique

14. Take a maximal object and ask what "cannot be improved" forces. Nine results below are that single idea.
15. In a maximal path both endpoints are trapped, meaning all their neighbours already lie on the path.
16. Only the endpoints. Interior vertices may have neighbours anywhere.
17. δ ≥ k gives a path on at least k+1 vertices, δ ≥ 2 gives a cycle, and δ ≥ k gives a cycle of length at least k+1.
18. δ ≥ 3 gives an even cycle, because three neighbours give three cycles and odd plus odd is even, so they cannot all be odd.
19. A connected graph has a path of length at least min{2δ, n−1}, and allowing a cycle improves that to min{2δ, n}.
20. Any two longest paths share a vertex.
21. Pigeonhole: two sets inside a box of size k whose sizes add past k must overlap.
22. Two crossing edges fold a path into a cycle, and reopening the cycle elsewhere builds a longer path.

## Counting

23. The degrees sum to 2m. The consequence is that the number of odd degree vertices is even.
24. Edge density m/n is half the average degree.
25. If m exceeds (n−1)(n−2)/2 then the graph is connected, and that bound is sharp.
26. Edge density k forces some subgraph with δ ≥ k. Strip low degree vertices and the density only rises. This is degeneracy, and it gives χ ≤ degeneracy + 1.
27. Large girth forces size. Girth at least 5 gives δ ≤ √(n−1), and a k regular graph of girth 5 needs at least k²+1 vertices, tight at the Petersen graph and at C₅.
28. Always rad ≤ diam ≤ 2·rad, and girth ≤ 2·diam + 1.
29. Diameter k with minimum degree d gives roughly kd/3 vertices, by taking every third vertex of a shortest path.

## Trees

30. A tree is equivalently connected and acyclic, has unique paths, is minimally connected, or is maximally acyclic.
31. A tree has n−1 edges, and a forest with c components has n − c.
32. Every tree on at least two vertices has a leaf.
33. Every tree has at least Δ(T) leaves, and with no vertex of degree 2 the leaves outnumber the internal vertices by at least 2.
34. For a maximum independent set in a tree, level splitting fails. Use greedy on leaves, or the dynamic program. Both are linear.
35. A leaf's edge lies in some maximum matching, and a leaf's parent lies in every one.
36. Trees are 1 degenerate and bipartite.

## Bipartite graphs

37. A graph is bipartite exactly when it has no odd cycle.
38. Bipartite means the vertex set splits into two parts, each inducing no edges.
39. A connected bipartite graph has a unique bipartition, up to swapping the names of the sides.
40. Colour by parity is the recurring trick: level parity, distance parity, and the parity of the number of ones.

## Matchings

41. A set S is independent exactly when its complement is a vertex cover. One set, two names.
42. Minimum edge covers decompose into stars.
43. An alternating path has edges alternating in and out of M. An augmenting path is alternating with both ends unmatched, which forces odd length.
44. Swapping along an odd path gains an edge, and along an even path it preserves the size. Both cases get used.
45. Berge says M is maximum exactly when no augmenting path exists. That makes optimality searchable, and every matching algorithm rests on it.
46. The union of two matchings has maximum degree 2, so it splits into alternating paths and even cycles. That one decomposition drives Berge, the universal vertex theorem, and Tutte.
47. König says a bipartite graph has α′ = β. The proof constructs a cover from alternating reachability out of the unmatched vertices.
48. Hall says a matching saturates A exactly when |N(S)| ≥ |S| for every S inside A. Proving existence needs every S, while disproving it needs only one starved S.
49. Defect Hall says |N(S)| ≥ |S| − k gives a matching of size at least |A| − k. Pad with k dummy vertices, then delete them.
50. Regularity gives Hall's condition, by counting edges out of a set two ways. This is the most reused argument in the unit.
51. A k regular bipartite graph has a perfect matching and splits into k of them, which makes bipartite graphs edge colourable in exactly Δ colours.
52. Every bipartite graph with an edge has a vertex lying in every maximum matching, and at least β such vertices. Odd cycles are the only obstruction, and an odd cycle has none.
53. A k factor is a spanning subgraph with all degrees k, so a 1 factor is a perfect matching.
54. Every 2k regular graph has a 2 factor, found by taking an Euler circuit, orienting along it, building the split vertex bipartite graph, and applying Hall. It fails for odd regularity.
55. There is no perfect matching when n is odd, or δ = 0, or some vertex has two neighbours of degree 1.
56. A bad set, meaning one with |S| < odd(G−S), certifies that no perfect matching exists, since each odd component must export a vertex into S.
57. Tutte says a perfect matching exists exactly when |S| ≥ odd(G−S) for every S, proved by passing to a maximal counterexample.
58. Outside bipartite graphs Hall's condition is the wrong invariant, because what matters is parity rather than neighbourhood size. The canonical witness is triangles hanging off a small hub.
59. Petersen says every bridgeless cubic graph has a 1 factor. Each odd component costs three edges and each vertex of S pays three, so the threes cancel.
60. Bridgelessness carries that whole hypothesis. A hub joined by three bridges to three odd blobs is cubic and of even order with no perfect matching.
61. One picture serves three theorems. König's construction gives the minimum cover, Hall's violating set, and the shape of a Tutte bad set.

## Euler circuits

62. An Euler circuit exists exactly when there is at most one non trivial component and every degree is even.
63. Each visit burns exactly two edges, one in and one out. That is the whole necessity argument.
64. A maximal trail must be closed, because an open trail leaves its endpoint with an odd count.
65. Isolated vertices are harmless, since an Euler circuit owes a visit to edges rather than to vertices.
66. Use the contrapositive. More than one non trivial component, or a single odd vertex, kills it. Königsberg has four odd vertices.
67. Euler is easy and Hamiltonian is NP complete, which is the difference between covering every edge and covering every vertex.

## Planarity

68. For a connected plane graph, n − m + f = 2.
69. A simple planar graph has m ≤ 3n−6, and a bipartite one has m ≤ 2n−4.
70. Check bipartiteness first. For Q₄ and K₃,₃ the general bound says nothing and only the bipartite one works.

## Traps

71. Two longest paths have exactly the same length.
72. α′ is a size, not a count of matchings.
73. The smaller side equals β only for complete bipartite graphs. Otherwise it is just an upper bound.
74. A cycle need not be a maximal trail, since edges may still hang off it.
75. Moon and Moser's bound counts maximal independent sets, and bounds how many there are.
76. König is 1936, Petersen 1891, and Tutte 1947. 1736 is Euler and Königsberg.

## The five techniques

77. Extremal choice. Take the longest, maximal or minimal thing.
78. Count two ways. Handshake and everything descended from it.
79. Parity. Odd plus odd is even, bipartiteness, odd components, and the difference between even and odd swap paths.
80. Exchange. Modify any optimum to agree with your greedy choice.
81. Maximal counterexample. Add edges until one more would fix the problem.
