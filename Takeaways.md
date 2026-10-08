---
tags: [academics, graph-theory, revision]
type: takeaways
---

# Takeaways, the distillation

Hub: [[Graph Theory]] · Full sheet: [[Revision Sheet]] · Depth: [[Master Notes]] · Shortest version: [[Bare Minimum]]

Statements only, no proofs. Ninety nine of them, readable in half an hour.

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

## Connectivity

82. G is k-connected when no set of fewer than k vertices separates it, and when G has more than k vertices. The second clause is what makes Kₙ exactly (n−1)-connected.
83. Always κ ≤ λ ≤ δ. Vertex connectivity is the smallest of the three.
84. δ ≥ (n−1)/2 forces connectedness, because {x}, N(x), {y} and N(y) would otherwise be four disjoint sets adding to n+1. Two disjoint cliques on n/2 vertices show the bound is sharp.
85. δ ≥ n/2 makes every pair adjacent or gives them a common neighbour, and by Dirac it forces a Hamiltonian cycle.
86. Dirac's proof is the long path theorem plus one step: any vertex off the folded cycle would have too few possible neighbours to avoid it.
87. Whitney. A graph on at least three vertices is 2-connected exactly when every pair has two internally vertex disjoint paths.
88. The easy half of Whitney is one sentence: a single deleted vertex lies on at most one of two internally disjoint paths.
89. The hard half inducts on distance and, in the awkward case, walks back from y and stops at the first vertex already used. Stopping at the first one is what makes the pieces disjoint.
90. Two cycles sharing a single vertex are 2-edge-connected but not 2-connected. Smallest example of κ < λ.
91. Adding a vertex joined to at least k old ones preserves k-connectedness.
92. Everything 2-connectedness buys comes from one trick: subdivide an edge to make it a vertex, or add a vertex joined to two targets, then apply Whitney and undo.
93. A block is a maximal connected subgraph with no cut vertex, which is not the same as a maximal 2-connected subgraph, because a bridge is a block.
94. The block graph of a connected graph is a tree, since a cycle in it would let you route around every cut vertex and merge the blocks.
95. Subdividing an edge never changes whether a graph is 2-connected.
96. An ear is open when its two ends differ and closed when they coincide. A graph on at least three vertices is 2-connected exactly when it has an open ear decomposition.
97. Openness carries that theorem: a closed ear hangs on one vertex, so deleting it strands the whole ear.
98. The k-connected characterisation is true but needs Menger. An induction on k does not close. It is proved in the Menger section below.
99. Two l-connected graphs union to an l-connected graph only when they share at least l vertices. Two triangles glued at a vertex are the counterexample.

## The five techniques

100. Extremal choice. Take the longest, maximal or minimal thing.
101. Count two ways. Handshake and everything descended from it.
102. Parity. Odd plus odd is even, bipartiteness, odd components, and the difference between even and odd swap paths.
103. Exchange. Modify any optimum to agree with your greedy choice.
104. Maximal counterexample. Add edges until one more would fix the problem.

## Menger and fans

105. Menger. For non-adjacent x and y, the least size of an x,y-separator equals the greatest number of internally disjoint x to y paths. The easy half is one separator vertex per path.
106. The hard half takes a minimum separator S, calls the side of x A and the rest B, contracts B and A to single vertices, applies induction to both smaller graphs and glues the paths at S. Every vertex of a minimum separator has neighbours on both sides, by minimality.
107. If every minimum separator is N(x) or N(y), either a vertex outside both neighbourhoods can be deleted, or the graph is x, y and their neighbourhoods, and König on the bipartite graph between the two neighbourhoods finishes it.
108. Global Menger. A graph with more than k vertices is k-connected exactly when every pair has k disjoint paths. An adjacent pair needs the step that G − xy is (k − 1)-connected.
109. A fan from x to U is k paths from x sharing only x and ending at distinct vertices of U. Dirac's fan lemma says k-connected is the same as a fan of size k from every x to every U with at least k vertices, and it needs more than k vertices because Kₖ satisfies the fan condition.
110. The forward half of the fan lemma adds a vertex joined to U, applies global Menger, and cuts each path at its first vertex in U.
111. In a k-connected graph any k vertices lie on a common cycle. Induct on the number of vertices, take a fan of size m from the new vertex to the old cycle, and two endpoints land in the same arc by pigeonhole. Kₖ,ₖ₊₁ shows k cannot be k + 1.
112. It is false that any a to b path can be completed by a second disjoint one. K₂,₃ is a counterexample.

## Colouring

113. A proper colouring has no monochromatic edge. χ ≤ k needs a colouring, and χ ≥ k needs a proof that no smaller colouring exists.
114. χ(Pₙ) = 2, χ(C₂ₙ) = 2, χ(C₂ₙ₊₁) = 3, χ(Kₙ) = n and every tree with an edge has χ = 2.
115. The odd cycle needs three colours because alternating colours forced round the cycle give both ends of the closing edge the same colour.
116. Minimum degree gives no lower bound on χ. Kᵣ,ᵣ has δ = r and χ = 2.
117. χ ≤ Δ + 1. Delete a vertex, colour the rest, and the vertex sees at most Δ colours.
118. Second proof by induction on Δ. Remove a maximal independent set of vertices of degree Δ. This lowers the maximum degree by at least one, so the rest takes Δ colours, and the removed set takes one more.
119. A graph is k-degenerate when every subgraph has a vertex of degree at most k. Then χ ≤ k + 1, by deleting a vertex of degree at most k and extending the colouring.
120. Degeneracy is found by repeatedly deleting a least degree vertex, and colouring in reverse order is a greedy colouring with at most degeneracy plus one colours.
121. The degeneracy is at least ω − 1 but cannot be bounded by a function of ω. Kᵣ,ᵣ has ω = 2 and degeneracy r. Graphs without even cycles and minimally 2-connected graphs are 2-degenerate.
122. χ ≥ ω, since a clique needs distinct colours, and χ ≥ n over α, since colour classes are independent sets that partition the vertices. For C₅ both together give 3.
