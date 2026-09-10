---
tags: [academics, graph-theory, revision]
type: minimum
exam: 2026-09-12
---

# Bare minimum

Hub: [[Graph Theory]] · Fuller version: [[Revision Sheet]] · Plan: [[Exam Plan 12 Sep]]

About four and a half hours of work, and you can stop after any section. This takes every cheap mark and skips the long constructions. It is a floor, not a ceiling: if the paper asks you to prove Tutte or the long path theorem in full, this will not carry you. Everything else it will.

Sections are ordered by value per minute, so if you run out of time, run out from the bottom.

## 1. Definitions, twenty minutes

Get these exactly right. Mixing them up loses marks you would otherwise have.

Length means number of edges. A path on m vertices has length m−1.

Walk repeats anything. Trail repeats vertices but never edges. Path repeats nothing. Circuit is a closed trail.

Maximal means cannot be extended. Maximum means none is bigger anywhere. They differ.

Induced subgraph: you pick vertices, and every edge between them comes along whether you like it or not. An induced path has no chords.

Empty graph means no edges, not no vertices.

α is the largest independent set. β is the smallest vertex cover. α′ is the largest matching. β′ is the smallest edge cover. Unprimed is vertices, primed is edges, α maximises, β minimises.

A k factor is a spanning subgraph with every degree k. A 1 factor is a perfect matching.

An odd component has an odd number of vertices. A bridge is an edge whose removal disconnects.

## 2. The numbers, twenty minutes

Pure memorisation, and almost certain to be worth marks.

| G | α′ | α | β |
|---|---|---|---|
| path on n | n/2 down | n/2 up | n/2 down |
| cycle on n | n/2 down | n/2 down | n/2 up |
| star | 1 | n−1 | 1 |
| complete on n | n/2 down | 1 | n−1 |
| complete bipartite k,l | min(k,l) | max(k,l) | min(k,l) |

α + β = n and α′ + β′ = n. Primes pair with primes.

α′ ≤ β ≤ 2α′, with equality on the left for bipartite graphs and on the right for the triangle.

Hypercube Qn: 2ⁿ vertices, n regular, n·2ⁿ⁻¹ edges, diameter n, girth 4, bipartite, Hamiltonian. Q4 is not planar.

κ ≤ λ ≤ δ always.

## 3. Statements only, thirty minutes

Learn to state these precisely. A correct statement often earns marks even without the proof.

Euler. A graph has an Euler circuit exactly when it has at most one non trivial component and every degree is even.

Berge. A matching is maximum exactly when no augmenting path exists.

König. In a bipartite graph the largest matching equals the smallest vertex cover.

Hall. A bipartite graph has a matching covering all of A exactly when every subset S of A satisfies |N(S)| ≥ |S|.

Tutte. A graph has a perfect matching exactly when every vertex set S satisfies |S| ≥ odd(G−S).

Petersen. Every bridgeless cubic graph has a perfect matching.

Long path. Every connected graph has a path of length at least min{2δ, n−1}.

Bipartite means no odd cycle.

## 4. The eight cheap proofs, ninety minutes

Each is under five lines. These are the best value in the whole course, because they cost almost nothing and get asked often.

Handshake. Count vertex and edge pairs two ways. Going vertex by vertex gives the degree sum, going edge by edge gives 2m. So the degree sum is 2m. Consequence: the number of odd degree vertices is even, since the odd degrees must sum to an even number.

α + β = n. A set is independent exactly when its complement is a vertex cover, because both say every edge has an end outside the set. So the largest independent set and the smallest cover are complements.

α′ ≤ β. A cover must meet every edge of a maximum matching, and those edges are disjoint, so it needs one distinct vertex for each. Hence at least α′ vertices.

β ≤ 2α′. Take both endpoints of a maximum matching. If some edge had neither end among them, you could add that edge to the matching, contradicting maximality. So they form a cover, of size 2α′.

δ ≥ 2 gives a cycle. Take a maximal path. Its last vertex has all neighbours on the path, and at least two of them. One is the vertex just before it, the other is further back. Close from there and you have a cycle.

Tree has n−1 edges. Induct. One vertex has no edges. Otherwise take a leaf, which exists because a tree with all degrees at least 2 would contain a cycle, delete it with its edge, apply the induction, and put it back.

Euler, easy half. Each visit to a vertex uses two edges, one in and one out. At the start vertex pair the first edge with the last. Since the circuit uses every edge, every degree is even.

Berge, easy half. Given an augmenting path, swap the edges on it. Interior vertices change partner, both ends were free, and the path has one more non matching edge than matching, so the matching grows by one.

## 5. Eight more short proofs, sixty minutes

Still short, still good value. The first five come from your own tutorial, which makes them the most likely of anything here to reappear.

Shortest paths are induced. If a chord joined two non consecutive vertices, you could cross it in one step instead of walking the stretch between them, giving a shorter path. So no chord exists.

Connected but not complete gives an induced path on three vertices. Not complete means two vertices are non adjacent, connected means a path joins them, and that path has length at least 2. Take its first three vertices. The first and third are not adjacent, or you could skip the middle one and shorten it.

Two longest paths share a vertex. If they were disjoint, join them by a shortest connecting path. Each longest path splits at its meeting point, and the longer half is at least half its length. Gluing the two longer halves onto the connector beats the maximum, which is impossible.

Girth five and k regular forces at least k squared plus one vertices. Count outward from any vertex: itself, its k neighbours, and for each neighbour its other k−1 neighbours. No triangle means the neighbours are not joined to each other, and no four cycle means those outer sets are disjoint. Adding up gives 1 + k + k(k−1).

Pairwise overlapping intervals share a point. Let a be the largest of all the left endpoints. Every interval starts at or before a by that choice, and a is at or before every right endpoint, because the interval owning a overlaps the one that ends soonest. So a lies in all of them.

k regular bipartite has a perfect matching. Edges leaving a set S number exactly k times the size of S, and they all land in N(S), which can absorb at most k times its own size. So N(S) is at least as big as S, and Hall applies. The two sides are equal because counting all edges from each gives k times each side.

Two connected gives a cycle. A vertex of degree 1 would be cut off by deleting its single neighbour, and a vertex of degree 0 disconnects the graph outright, so the minimum degree is at least 2. Then the earlier lemma gives a cycle.

An odd cycle stops a graph being bipartite. Walking a cycle alternates between the two sides, so the vertex at position t sits on the starting side exactly when t is odd. Closing the cycle requires the last vertex to be on the opposite side to the first, which only happens when the length is even.

## 6. Which theorem to reach for, fifteen minutes

Under time pressure the hard part is often knowing which result applies. Read the question, then match.

Does a perfect matching exist? If bipartite use Hall. If general use Tutte. If cubic and bridgeless quote Petersen.

Is this matching maximum? Berge. Look for an augmenting path, and if none exists it is maximum.

Largest matching versus smallest cover? König, but only if the graph is bipartite. In general you only get the sandwich.

Does an Euler circuit exist? Check every degree is even and the edges lie in one component. To rule one out, find a single odd vertex.

Show a long path or a long cycle exists? Extremal method. Take a maximal path and use the fact that both endpoints have all their neighbours on it.

Show a graph is bipartite? Either exhibit a two colouring, or show it has no odd cycle. For a concrete graph, colour by distance parity from any vertex.

Is it planar? Compare the edge count against 3n−6, and if the graph is bipartite against 2n−4 instead, which is the sharper test.

Something about a tree? Reach for n−1 edges, unique paths, or the existence of a leaf.

Need to count something? Handshake, or count one quantity two ways.

Need an even something? Parity. Build several objects and use odd plus odd is even.

## 7. Proof shapes, twenty minutes

Do not learn these in full. Learn one sentence each, so you can write the idea and pick up partial credit.

Long path theorem. Take a longest path, both endpoints are trapped, their neighbour positions form two sets too big to avoid overlapping, the overlap gives two crossing edges that fold the path into a cycle, and a vertex off that cycle builds a longer path.

Euler, hard half. Take a trail you cannot extend. It must be closed, because an open trail leaves its endpoint with an odd count. Being closed it can be restarted anywhere, so any leftover edge would extend it.

König. Take a maximum matching, grow alternating paths out of the unmatched side, and the cover is the reachable half of B together with the unreachable half of A.

Tutte, hard half. Add edges until one more would create a perfect matching, take the universal vertices as S, then split on whether what remains is a union of cliques.

Petersen. In a cubic graph every odd component must send out an odd number of edges, not one because that would be a bridge, so at least three. Each vertex of S can host three. The threes cancel.

## 8. Traps, fifteen minutes

These are errors you have actually made. Fixing them is free marks.

Two longest paths have exactly the same length.

α′ is the size of a maximum matching, not the number of matchings.

The smaller side equals β only for complete bipartite graphs. Otherwise it is just an upper bound.

A cycle need not be a maximal trail, since edges may hang off it.

For planarity, check bipartiteness first. Q4 and K3,3 both pass the general test and fail the bipartite one.

Moon and Moser counts maximal independent sets, and bounds how many there are.

König 1936, Petersen 1891, Tutte 1947.

A is a filter, not a stretch. Several separate vertices join v0, at scattered positions.

## If time runs short

Two hours: sections 1, 2 and 4. Definitions, numbers, and the eight short proofs. These cover the parts of a paper that are cheapest to answer.

Three hours: add section 5. The tutorial results in it are the single most likely thing here to reappear, since they came from your own tutorial sheet.

Four hours: add sections 6 and 8. Knowing which theorem applies, and not making the errors you have made before, both convert directly into marks.

Section 7 last. Proof shapes only earn partial credit, so they are the first thing to drop.
