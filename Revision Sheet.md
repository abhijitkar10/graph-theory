---
tags: [academics, graph-theory, revision]
type: revision
---

# One day revision sheet, everything taught 24 July to 31 August

Hub: [[Graph Theory]] · Depth: [[Master Notes]] · Shortest version: [[Bare Minimum]]

Each entry gives the statement and the idea of the proof. Follow a link only when the idea does not land on its own.

A workable day: sections 1 and 2 in half an hour, section 3 in forty five minutes, sections 4 to 6 in an hour, section 7 on matchings in two hours, sections 8 to 11 in three quarters of an hour.

## Notation

The course uses West's letters. α means packing and you maximise, β means covering and you minimise. Unprimed refers to vertices, primed to edges.

| | vertices | edges |
|---|---|---|
| packing, maximise | α, independence number | α′, matching number |
| covering, minimise | β, vertex cover number | β′, edge cover number |

The two Gallai identities are α + β = n and α′ + β′ = n, the second needing no isolated vertices. Primes pair with primes. Some books write ν for α′ and τ for β, which are the same objects.

## 1. Definitions not to confuse

| Term | Repeats vertices | Repeats edges |
|---|---|---|
| walk | yes | yes |
| trail | yes | no |
| path | no | no |
| circuit | yes | no, and closed |

Length counts edges, not vertices, so a path on m vertices has length m−1.

Maximal means it cannot be extended. Maximum, or longest, means nothing bigger exists anywhere in the graph. The gap matters computationally, since finding a maximal object is easy and finding a longest path is NP complete.

An induced subgraph keeps every edge whose ends you kept. An induced path therefore has no chords.

δ is the minimum degree, Δ the maximum degree, and ε = m/n is the edge density, which is half the average degree.

An odd component is a component with an odd number of vertices, and odd(H) counts them. A k factor is a spanning subgraph in which every degree is k, so a 1 factor is a perfect matching. A bridge is an edge whose removal increases the number of components.

## 2. Numbers to know cold

| G | α′ | α | β = n−α | is α′ = β |
|---|---|---|---|---|
| Pₙ | ⌊n/2⌋ | ⌈n/2⌉ | ⌊n/2⌋ | yes |
| Cₙ | ⌊n/2⌋ | ⌊n/2⌋ | ⌈n/2⌉ | yes when even, no when odd |
| star K₁,ₙ | 1 | n−1 | 1 | yes |
| Kₙ | ⌊n/2⌋ | 1 | n−1 | no |
| K(k,l) | min(k,l) | max(k,l) | min(k,l) | yes |

Equality holds exactly on the bipartite entries, and that pattern is König.

The hypercube Qₙ has 2ⁿ vertices, is n regular, has n·2ⁿ⁻¹ edges, diameter n, girth 4, a Hamiltonian cycle, and is bipartite by the parity of the number of ones. Q₄ is not planar.

Connectivity values worth remembering: a path has κ = λ = 1, a cycle has 2 and 2, Kₙ has n−1, K(m,n) has min(m,n), and Qₙ has n. Always κ ≤ λ ≤ δ.

## 3. The extremal method, the one technique

Take a maximal, longest or minimal object, then ask what "cannot be improved" forces to be true.

The recurring consequence is trapped endpoints. In a maximal path every neighbour of either endpoint lies on the path, since otherwise you could extend. This applies only to the endpoints. Interior vertices are free to have neighbours anywhere.

| Result | Idea |
|---|---|
| δ ≥ k gives a path on at least k+1 vertices | the endpoint's k neighbours all sit on the path, plus the endpoint itself |
| δ ≥ 2 gives a cycle | the endpoint has a second neighbour back along the path, close it up |
| δ ≥ k gives a cycle of length at least k+1 | take the furthest neighbour of the endpoint |
| δ ≥ 3 gives an even cycle | three neighbours give cycles of lengths a+2, b+2 and a+b+2, and odd plus odd is even, so they cannot all be odd |
| connected gives a path of length at least min{2δ, n−1} | the six claims below |
| a path or cycle of length at least min{2δ, n} | the same proof, where the cycle turns out to be spanning |
| two longest paths share a vertex | otherwise glue half of each onto a connecting path and beat the maximum |
| Helly for intervals | take the largest left endpoint, and one well chosen pair proves it is at most the smallest right endpoint |

### The long path theorem in six claims

Let P = v₀ … vₖ be a longest path, of length k.

1. Both endpoints are trapped.
2. Let A be the set of positions i with v₀ adjacent to vᵢ, and B the set of positions i with vₖ adjacent to vᵢ₋₁. Both sit inside {1, …, k} and both have at least δ members.
3. If k ≤ 2δ−1 then the two sizes add to at least 2δ, which exceeds k, so by pigeonhole they overlap at some position i.
4. That overlap gives crossing edges v₀vᵢ and vₖvᵢ₋₁, which fold P into a cycle through all k+1 vertices.
5. From k ≤ n−2 there is a vertex off the cycle.
6. Snip the cycle open at a vertex adjacent to that outside vertex and attach it, giving a path of length k+1, which contradicts maximality.

The −1 in the definition of B does two jobs. It aligns the two crossing edges so the fold works, and it keeps both sets inside the same box of size k so pigeonhole applies.

## 4. Counting and density

The handshake lemma says the degrees sum to 2m. Its corollary, that the number of odd degree vertices is even, gets used constantly.

Edge density is ε = m/n, which is half the average degree.

If m exceeds (n−1)(n−2)/2 then G is connected, and that bound is sharp, since Kₙ₋₁ plus an isolated vertex sits just below it.

Density k forces a subgraph with minimum degree at least k. Repeatedly delete a vertex of degree below k. Each deletion strictly raises the density, by at least 1/(n−1), and the graph is finite so the process stops. It cannot strip the graph bare, because a single vertex has density 0 while the density only ever rose. This quantity is the degeneracy, and it gives the colouring bound χ ≤ degeneracy + 1.

If m exceeds k(n−1) then G has a (k+1) edge connected subgraph, found by taking a minimal subgraph H with e(H) > k(|H|−1).

Girth conditions force room, and the count is the same every time. Take {v}, then N(v), then the outer neighbours, and no C₃ or C₄ means those groups are disjoint.

Girth at least 5 gives δ ≤ √(n−1), and a k regular graph of girth 5 needs at least k²+1 vertices, which is tight at the Petersen graph and at C₅. Radius and diameter satisfy rad ≤ diam ≤ 2·rad, and girth ≤ 2·diam + 1, tight at odd cycles. A graph of diameter k and minimum degree d has roughly kd/3 vertices, proved by taking every third vertex of a shortest path so their neighbourhoods stay disjoint.

## 5. Trees

Four conditions are equivalent: connected and acyclic, unique paths between every pair, minimally connected, maximally acyclic.

Every tree on at least two vertices has a leaf, since otherwise every degree is at least 2 and section 3 produces a cycle.

A tree has n−1 edges, proved by induction after deleting a leaf. A forest with c components has n − c edges.

A tree has at least Δ(T) leaves. Delete a vertex of maximum degree, which leaves Δ components, and each contributes a leaf.

If a tree has no vertex of degree 2 then the number of leaves is at least the number of internal vertices plus 2. Handshake gives 2(n−1) ≥ L + 3I, and n = L + I.

Forest exchange: if a forest F has fewer edges than a forest F′, some edge of F′ can be added to F. The reason is that F has more components.

For a maximum independent set in a tree, splitting by level fails. Two methods work. Greedy takes all the leaves, deletes their parents, and recurses, justified by an exchange argument that swaps a parent out for a leaf. Dynamic programming sets MIS(v, 0) as the sum over children of max{MIS(u,0), MIS(u,1)} and MIS(v, 1) as 1 plus the sum of MIS(u,0), running in linear time.

A leaf's parent lies in every maximum matching, while a leaf's edge lies in some maximum matching. Different quantifiers, different strength.

## 6. Bipartite graphs

A graph is bipartite exactly when it has no odd cycle. For the harder direction, root each component and split the vertices by the parity of their distance from the root.

In a connected bipartite graph the bipartition is unique up to swapping the names of the sides, because all paths from a fixed root to a given vertex have the same parity of length.

The colour by parity trick recurs: level parity in trees, distance parity in bipartite graphs, and the count of ones in the hypercube.

## 7. Matchings, the heart of the exam

### 7.1 The parameter web

A set S is independent exactly when its complement is a vertex cover, and that single observation gives α + β = n.

The other identity, α′ + β′ = n, needs no isolated vertices. Extend a maximum matching to an edge cover by giving each uncovered vertex one edge, and note that a minimum edge cover is a union of stars.

Also α(G) equals the clique number of the complement.

The sandwich α′ ≤ β ≤ 2α′ holds in every graph. The lower bound holds because matching edges are disjoint so a cover needs one vertex per matching edge. The upper bound holds because the endpoints of a maximum matching form a cover. The lower end is equality for every bipartite graph, by König, and the upper end is equality at the triangle. That upper half is the standard 2 approximation for vertex cover.

Finally α′ ≤ ⌊n/2⌋, since matching edges are disjoint.

### 7.2 Augmenting paths

An M alternating path has edges alternating in and out of M. An M augmenting path is alternating with both endpoints unmatched, which forces odd length.

Swapping along an augmenting path gains exactly one edge. Swapping along an even alternating path preserves the size. Both behaviours get used, so keep the parity straight.

Berge's theorem says M is maximum exactly when no M augmenting path exists. For the substantive direction, take any N with more edges than M. In the union, every degree is at most 2, so the components are paths and even cycles with edges alternating between the two matchings. Only an odd length path can carry a surplus, and the one that does has both end edges in N, which makes it M augmenting. The proof needs N larger than M, not maximum.

The algorithm follows: while an augmenting path exists, swap along it. Each pass adds one edge, so it halts in at most ⌊n/2⌋ rounds, and Berge is what makes the halting condition correct.

### 7.3 König, know one proof

If G is bipartite then α′(G) = β(G). Three routes exist, and one is enough.

By alternating reachability. Let A₀ be the unmatched vertices of A, let B₁ be the vertices of B reachable from A₀ along alternating paths, let A₁ be their matching partners, and let A₂ be the rest of A. Then B₁ together with A₂ is a cover of size α′. Three kinds of edge would escape it and all three are impossible: an edge from A₁ to an unmatched vertex of B would complete an augmenting path, and edges from A₀ or A₁ to B₂ would have put their target in B₁ instead.

By induction on n. Take the vertex x lying in every maximum matching, from section 7.5. Deleting it drops the matching number by exactly one, and a minimum cover of G − x together with x covers G.

From Hall's theorem.

One picture does three jobs. The same A₀, A₁, A₂, B₁, B₂ diagram supplies König's cover, Hall's violating set A₀ ∪ A₁, and the shape of a bad set for Tutte.

### 7.4 Hall

A bipartite graph has a matching saturating A exactly when every subset S of A satisfies |N(S)| ≥ |S|.

The easy direction is immediate, since each vertex of S has its own distinct partner inside N(S). For the other direction, argue the contrapositive using König: take a minimum cover K, let S be the part of A outside K, and the counting gives |N(S)| < |S|. The violating set is A₀ ∪ A₁ from the König picture.

The defect version says that if |N(S)| ≥ |S| − k for every S, then a matching of size at least |A| − k exists. Add k dummy vertices joined to all of A, which repairs Hall's condition, apply Hall, then delete the at most k edges that used a dummy. Equivalently α′ equals |A| minus the largest deficiency.

Every k regular bipartite graph with k ≥ 1 has a perfect matching. Count the edges leaving a subset S of A in two directions: exactly k|S| leave, and N(S) can absorb at most k|N(S)|, so Hall's condition holds. The two sides also have equal size, by the same count applied globally.

It follows by induction that a k regular bipartite graph splits into k disjoint perfect matchings, since removing one leaves a (k−1) regular bipartite graph. Colouring each matching separately shows bipartite graphs need exactly Δ colours on their edges, never the extra one.

Systems of distinct representatives are Hall's theorem relabelled, and the Latin rectangle extension theorem is the same argument, since the free symbols form an (n−r) regular bipartite graph.

### 7.5 A vertex in every maximum matching

Every bipartite graph with at least one edge has a vertex lying in every maximum matching. Note the quantifiers: one vertex that works for all maximum matchings, not merely a vertex in each.

Suppose not. Take a vertex u and a maximum matching M missing it, a neighbour x, which M must match, and a maximum matching N missing x. In the union of M and N both u and x have degree 1, so both are endpoints of paths, and all paths are even since the two matchings have equal size. Swap along the path at u, which keeps both maximum and leaves u unmatched by the new N. If x is also unmatched, the edge ux augments, which is impossible. If x is matched, then x lay on that path, so the path runs from u to x with even length, and adding ux closes an odd cycle, which a bipartite graph cannot contain.

Bipartiteness is used only in that final step. Odd cycles are the only obstruction, and indeed an odd cycle looks the same from every vertex so it has no such vertex.

In a tree, a leaf's parent qualifies, in two lines.

The class exercise strengthens this to at least β such vertices, peeling one off and inducting through König.

### 7.6 Factors

A k factor is a spanning subgraph with every degree k, so a 1 factor is a perfect matching and a 2 factor is a set of cycles covering every vertex.

Every 2k regular graph has a 2 factor, with no bipartiteness needed. Take an Euler circuit, which exists because every degree is even, and orient every edge along the direction of travel, giving each vertex k edges in and k out. Split each vertex into an out copy and an in copy to build a bipartite graph, which is k regular and so has a perfect matching by the previous section. Mapping that matching back touches every original vertex twice, giving a 2 factor.

The statement fails for odd regularity, since a complete graph on an odd number of vertices has no perfect matching at all.

### 7.7 Tutte

Three quick reasons a perfect matching cannot exist: n is odd, some vertex is isolated, or some vertex has two neighbours of degree 1.

A set S is bad when |S| < odd(G − S), and a bad set rules out a perfect matching. Each odd component must send a vertex out into S, and different components send theirs to different vertices, so S must be large enough.

Tutte's 1-factor theorem, from 1947, says a graph has a perfect matching exactly when |S| ≥ odd(G − S) for every S.

The hard direction runs in three moves.

First, pass to a maximal counterexample. Add edges until one more would create a perfect matching, giving H. The condition survives, because deleting edges only splits components and an odd component always splits into at least one odd piece.

Second, let S be the set of universal vertices of H.

Third, split into cases. If H − S is a disjoint union of cliques, then |S| and odd(H − S) have the same parity because n is even. Match one vertex of each odd clique into S, pair the rest of each clique internally, and pair the leftover vertices of S among themselves, which works because that leftover count is even. If H − S is not a union of cliques, some component contains two non adjacent vertices, and the first three vertices of a shortest path between them form an induced path a, b, c. The middle vertex b is not universal, so some x is not adjacent to it. Maximality gives a perfect matching using ac and another using bx, and superimposing them gives even cycles along which you can re-pair to avoid ac. Either case produces a perfect matching in H, which is a contradiction.

Hall's condition measures the wrong thing outside bipartite graphs, since what matters is parity rather than neighbourhood size. The canonical picture is several triangles hanging off a small hub S, where each triangle must export a vertex into S.

The empty set is bad exactly when n is odd.

### 7.8 Petersen

Every bridgeless cubic graph has a perfect matching, proved by checking Tutte's condition directly.

With S empty, summing degrees inside a component gives three times its order equal to twice its edge count, so every component has even order and there are no odd components at all.

With S non empty, take an odd component C. Summing degrees over C gives 3|V(C)| = 2e(C) + e(C, S), and the left side is odd while the first term on the right is even, so the number of edges leaving C is odd. It cannot be 1, because that edge would be a bridge, and it cannot be 2 by parity, so it is at least 3. Every vertex of S hosts at most 3 departing edges, so 3|S| is at least 3·odd(G − S), giving the condition.

The two threes cancel, and bridgelessness is used in exactly one place. Drop it and the theorem fails: a hub joined by three bridges to three odd blobs is cubic and of even order but has no perfect matching.

## 8. Euler circuits

A graph has an Euler circuit exactly when it has at most one non trivial component and every degree is even.

For the necessary direction, each visit to a vertex burns two edges, one in and one out, and at the starting vertex the first edge pairs with the last, so every degree is even.

For the sufficient direction there are two proofs. By induction on edges, pull out a cycle, which keeps every degree even, recurse on the components, and splice the pieces back in as detours. By the extremal method, which is shorter, take a maximal trail. It must be closed, because an open trail uses an odd number of edges at its final endpoint, clashing with even degree. And it must use every edge, because being closed it can be restarted at any of its vertices, so a leftover edge touching it would extend it.

Use the contrapositive when you want to rule out an Euler circuit. Negating a conjunction gives a disjunction, so more than one non trivial component or a single odd vertex is enough. Königsberg has four odd vertices.

Isolated vertices are harmless, because an Euler circuit owes a visit to edges, not to vertices.

Euler and Hamiltonian look similar and are not. Covering every edge has an easy degree test, and covering every vertex is NP complete.

## 9. Tutorial 1 results

A k regular graph of girth at least 5 has at least k²+1 vertices, tight at the Petersen graph and at C₅.

A connected graph that is not complete contains an induced path on three vertices, found among the first three vertices of a shortest path between two non adjacent vertices.

Shortest paths are induced, because a chord would shorten them. These last two are one idea used twice.

Two longest paths in a connected graph share a vertex.

The one dimensional Helly property: finitely many pairwise intersecting closed intervals share a point, namely the largest of their left endpoints. Closedness and finiteness both matter.

Q₄ is not planar. It has 16 vertices and 32 edges, and the bipartite bound gives at most 2n − 4 = 28. The general bound 3n − 6 = 42 says nothing, so check bipartiteness first. Q₃ sits exactly at its own limit with 12 edges against a bound of 12, and it is planar.

Euler's formula is n − m + f = 2, giving m ≤ 3n − 6 for simple planar graphs and m ≤ 2n − 4 when there are no triangles.

## 12. Connectivity

Taught after the exam, so this section is newer than the rest of the sheet. Full versions in [[2026-08-31 Connectivity 1 — Minimum Degree and Whitney's Theorem]] and [[2026-08-31 Blocks, Ear Decomposition, and k-Connectivity]].

G is k-connected when no set of fewer than k vertices separates it and G has more than k vertices. That second clause is easy to drop and matters: it is what makes Kₙ exactly (n−1)-connected. Always κ ≤ λ ≤ δ.

If δ ≥ (n−1)/2 then G is connected, because otherwise {x}, N(x), {y} and N(y) would be four disjoint sets adding to n+1. Sharp: two disjoint copies of K on n/2 vertices have δ = (n−2)/2 and fall apart.

If δ ≥ n/2 then every pair is adjacent or shares a neighbour, and by Dirac there is a Hamiltonian cycle. Dirac's proof is the long path theorem with one extra step forcing every stray vertex onto the folded cycle.

Whitney. A graph on at least three vertices is 2-connected exactly when every pair has two internally vertex disjoint paths. Easy direction: one deleted vertex sits on at most one of two disjoint paths. Hard direction: induct on dist(x,y), take the vertex v just before y, get two paths to v, and if y misses them both, walk back from y and stop at the first vertex already used.

Two cycles sharing one vertex are 2-edge-connected but not 2-connected. Smallest example worth memorising, and it doubles as the counterexample to the union lemma.

2-connectedness gives four things, all by the same trick of subdividing an edge into a vertex or adding a vertex joined to two targets, then applying Whitney: any two vertices on a common cycle, a vertex and an edge, two edges, and two paths from w reaching x and y separately.

A block is a maximal connected subgraph with no cut vertex, not a maximal 2-connected subgraph, because bridges are blocks too. The block graph of a connected graph is a tree.

Subdividing an edge never changes 2-connectedness. An ear of H is a path with both ends in H and its interior outside; trivial means a single edge, open means the two ends differ. A graph on at least three vertices is 2-connected exactly when it has an open ear decomposition, and openness is what stops one deleted vertex from stranding an ear.

The k-connected version, that k-connected means k disjoint paths between every pair, is Menger's theorem in its global form. Menger. For non-adjacent x and y the least separator size equals the greatest number of internally disjoint paths. Easy half, one separator vertex per path. Hard half, induction on n. Take a minimum separator S, A the side of x and B the rest, contract B to β and A to α, apply induction to both smaller graphs to get k paths from x to S and from S to y, and glue. If every minimum separator is N(x) or N(y), either some vertex outside both neighbourhoods can be deleted, or the graph is x, y and their neighbourhoods and König on the bipartite graph between them finishes it. For adjacent pairs delete the edge and use (k − 1)-connectivity. Two l-connected graphs union to an l-connected graph only when they share at least l vertices.

Fans. An (x,U)-fan of size k is k paths from x sharing only x and ending at distinct vertices of U. Dirac's fan lemma. With more than k vertices, G is k-connected exactly when every x and every U with at least k vertices have a fan of size k. Forward, add a vertex joined to U and apply global Menger. Backward, a fan to N(y) extended by edges gives k disjoint x to y paths. Kₖ shows the vertex count is needed. Cycle through any k vertices of a k-connected graph, by induction with a fan of size m and pigeonhole on arcs, sharp at Kₖ,ₖ₊₁.

## 13. Colouring

A proper colouring has no monochromatic edge, and χ is the least number of colours. χ(Pₙ) = 2, χ(C₂ₙ) = 2, χ(C₂ₙ₊₁) = 3, χ(Kₙ) = n, trees have χ = 2. Odd cycle, alternation is forced round the cycle and the closing edge clashes.

χ ≤ Δ + 1. Delete a vertex, colour the rest, the vertex sees at most Δ colours. Second proof, induct on Δ, remove a maximal independent set of degree Δ vertices, spend one new colour on it. Degenerate means every subgraph has a vertex of degree at most k, and then χ ≤ k + 1 by the same deletion. Degeneracy is found by repeated least degree deletion, and the reverse order is a greedy colouring. Degeneracy is at least ω − 1 but not bounded by any function of ω, since Kᵣ,ᵣ has ω = 2 and degeneracy r.

Lower bounds. χ ≥ ω. χ ≥ n over α, because colour classes are independent sets that partition V. Minimum degree gives nothing, since Kᵣ,ᵣ has δ = r and χ = 2. Traps. The classes partition, they do not merely cover. W₂ₙ means 2n vertices counting the hub.

## 10. Technique checklist

1. Extremal choice. Take a longest, maximal or minimal object and ask what cannot be improved.
2. Count two ways. Handshake, and counting edges out of a set from both sides.
3. Pigeonhole. Two sets inside a box of size k whose sizes add past k must overlap.
4. Parity. Odd plus odd is even, bipartiteness, the parity of a swap, odd components.
5. Exchange. Modify any optimum to agree with your greedy choice without losing size.
6. Superimpose two matchings. Every degree is at most 2, so you get paths and even cycles. Berge, the universal vertex theorem and Tutte all use this.
7. Maximal counterexample. Add edges until one more would fix the problem.
8. Contrapositive and De Morgan.
9. Shortest forbids shortcuts.

## 11. Traps

| Trap | The right answer |
|---|---|
| Do two longest paths have the same length | Yes, always. A maximum is one number |
| Is α′ the number of matchings | No, it is the size of a largest one |
| Is there a formula for a matching in a tree from its depth | No. A star has matching number 1 at any depth |
| Is min{\|A\|, \|B\|} the cover number | Only for complete bipartite graphs. Otherwise it is just an upper bound |
| Is a cycle a maximal trail | Not necessarily. Edges may still hang off it |
| Does level splitting give a maximum independent set in a tree | No. Use greedy on leaves, or dynamic programming |
| Does 3n − 6 settle whether Q₄ is planar | No. It is far too weak. Use 2n − 4 |
| What does Moon and Moser count | Maximal independent sets, and how many there are |
| Dates | Tutte 1947, König 1936, Petersen 1891. 1736 is Euler and Königsberg |

## If time runs out, the five to be able to reproduce

1. The long path theorem, the six claims in section 3.
2. Berge, section 7.2.
3. König, any one proof, section 7.3.
4. Tutte, the statement and the three moves, section 7.7.
5. Euler, the maximal trail proof, section 8.
