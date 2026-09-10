---
tags: [academics, graph-theory, lecture]
date: 2026-08-10
seq: 8
class: 5
---

# 8 · 2026-08-10 — König by induction, Hall, and factors

Previous: [[2026-08-10 Matchings in Bipartite Graphs]] · Hub: [[Graph Theory]] · Next: [[2026-08-19 Tutte's 1-Factor Theorem]]

Same session as the previous note, continued. Split into its own file because the material is long.

## How much this matters

Overall this note is core, entirely because of Hall.

Know cold: [[2026-08-10 König by Induction, Hall, and Factors#Hall's theorem|Hall's theorem]], both the statement and the easy direction, and [[2026-08-10 König by Induction, Hall, and Factors#Regular bipartite graphs|regular bipartite graphs have a perfect matching]]. That second proof is only a two way count and it is excellent value.

Know the statement: [[2026-08-10 König by Induction, Hall, and Factors#When a perfect matching cannot exist|the three obstructions]] to a perfect matching, and [[2026-08-10 König by Induction, Hall, and Factors#The defect version|the defect version]] of Hall with its padding trick.

Know the idea: [[2026-08-10 König by Induction, Hall, and Factors#A third proof of König|König by induction]], but only if you have not already learned another proof of König. One is enough.

Read once: [[2026-08-10 König by Induction, Hall, and Factors#Factors|factors and the 2 factor theorem]]. A nice result, but it sits at the edge of the syllabus and the proof is long.

## Notation

α′(G) is the matching number and β(G) the vertex cover number, as in [[2026-07-29 Matchings 2 — Berge and König]]. For a set S of vertices, N(S) is the set of all vertices adjacent to something in S. A matching saturates a set A when every vertex of A is matched.

A spanning subgraph is one that keeps every vertex and drops only edges. A k factor is a spanning subgraph in which every vertex has degree exactly k. A 1 factor is the same thing as a perfect matching.

## A third proof of König

Theorem. If G is bipartite then α′(G) = β(G).

Given: G is bipartite.
To show: the largest matching and the smallest vertex cover have the same size.

I now have three proofs of this. The two earlier ones construct a cover out of alternating reachability. This one does no construction at all, and instead peels off one vertex and recurses. It is the shortest, but it leans on the universal vertex theorem from [[2026-08-10 Matchings in Bipartite Graphs]], which is itself real work.

Induct on the number of vertices.

With one vertex there are no edges, so both numbers are zero.

Now suppose the result holds for every bipartite graph on at most k vertices, and let G be bipartite on k+1 vertices. By the universal vertex theorem there is a vertex x lying in every maximum matching. Put H equal to G with x deleted, which is bipartite on k vertices, so by the induction hypothesis its matching and cover numbers agree.

Deleting x drops the matching number by exactly one. Removing x's edge from a maximum matching of G leaves a matching of H one smaller, so H's matching number is at least that. And it cannot be larger, because a matching of H of the full size would be a maximum matching of G that avoids x, contradicting the choice of x.

Now take a minimum vertex cover S of H, whose size equals H's matching number. It covers every edge of H, and the only edges of G it might miss are those touching x, since x is the only vertex removed. So adding x to S covers all of G.

That gives a cover of G whose size is H's matching number plus one, which is G's matching number. So β(G) is at most α′(G), and combined with the general inequality the two are equal.

## When a perfect matching cannot exist

Three quick obstructions worth having as reflexes.

If n is odd there is no perfect matching, since pairing vertices up leaves one over.

If the minimum degree is zero there is none either, because an isolated vertex has no possible partner.

If some vertex has two neighbours of degree one, there is none. Both of those leaves can only ever be matched to that one vertex, and it takes a single partner.

## Hall's theorem

Theorem. Let G be bipartite with parts A and B. There is a matching saturating A if and only if for every subset S of A, the size of N(S) is at least the size of S.

The condition is called Hall's condition. In the marriage reading, A is a set of people, B the possible partners, and edges mean willingness. Everyone in A can be matched exactly when no group of k people between them know fewer than k candidates.

One direction is quick. If a matching saturates A, then for any S each vertex has its own partner, all of them lie in N(S), and they are distinct because it is a matching, so N(S) has at least as many members as S.

For the other direction it is easiest to argue the contrapositive, that if no matching saturates A then some set violates the condition. Suppose the matching number is smaller than the size of A. By König the cover number is too. Take a minimum cover K and let S be the part of A outside K. Every edge leaving S must be covered on the B side, since its A end is not in K, so N(S) sits inside the part of K lying in B. Counting, the size of N(S) is at most the cover number minus the number of cover vertices in A, while the size of S is the size of A minus that same quantity. Since the cover number is below the size of A, subtracting the same amount from both keeps the inequality, and N(S) comes out strictly smaller than S.

The set that violates the condition is exactly A0 together with A1 from the König construction in [[2026-07-29 Matchings 2 — Berge and König]]. The same picture yields the cover for König and the starved set for Hall.

## The defect version

Theorem. If the size of N(S) is at least the size of S minus k for every subset S of A, then G has a matching of size at least the size of A minus k.

The trick is to repair the condition artificially and then undo the repair. Add k brand new vertices to B, each joined to every vertex of A. In the enlarged graph any non empty S gains all k new neighbours, so its neighbourhood grows by k and Hall's condition now holds. Hall then gives a matching saturating A, of size the size of A.

At most k of its edges can use a new vertex, since there are only k of them and each is used once. Deleting those leaves a genuine matching of the original graph, of size at least the size of A minus k.

This is the same result as in [[Lec 03 — More on Hall's Theorem and Applications]], where it is stated with the largest deficiency in place of k.

## Regular bipartite graphs

Theorem. Every k regular bipartite graph with k at least one has a perfect matching.

Count the edges leaving a set two ways. Take any subset S of A. Every vertex of S has degree exactly k and all of its edges leave S, since S sits inside A and edges only go to B, so exactly k times the size of S edges leave. All of them land in N(S), and each vertex of N(S) has total degree k, some of which may go elsewhere, so N(S) can receive at most k times its own size. Comparing the two gives Hall's condition.

So a matching saturating A exists. The two sides also have equal size, because counting all edges from each side gives k times the size of A and k times the size of B. A matching saturating A between equal parts is perfect.

A consequence by induction: a k regular bipartite graph splits into k disjoint perfect matchings. Remove one perfect matching and every vertex loses exactly one edge, leaving a k−1 regular bipartite graph, so repeat. Colouring each perfect matching separately shows that bipartite graphs need exactly Δ colours for their edges, never the extra one that general graphs can require.

## Factors

A k factor is a spanning subgraph with every degree equal to k. A 1 factor is a perfect matching, and a 2 factor is a collection of cycles covering every vertex.

Theorem. Every 2k regular graph has a 2 factor.

This needs no bipartiteness, and the proof reaches back to Euler circuits.

Every vertex has degree 2k, which is even, so assuming the edges lie in one non trivial component the graph has an Euler circuit by the theorem in [[2026-07-27 Euler Circuits]].

Traverse that circuit and orient every edge in the direction you travelled. Each time the circuit passes through a vertex it enters once and leaves once, and it uses all 2k edges there, so every vertex ends with exactly k edges in and k out.

Now build a bipartite graph from two copies of the vertex set, one copy for outgoing and one for incoming. For each oriented edge from u to v, put an edge between u's out copy and v's in copy. Every out copy then has degree k, being the outgoing edges of that vertex, and every in copy has degree k likewise. So this graph is k regular bipartite, and by the previous section it has a perfect matching.

Map that matching back to the original edges. Every vertex of the original graph is touched twice, once through its out copy and once through its in copy, so the selected edges form a spanning subgraph with every degree equal to two. That is a 2 factor.

The analogous statement fails for odd regularity. A complete graph on an odd number of vertices is regular of even degree yet has no perfect matching at all, since its order is odd.

## What to remember

Removing a universal vertex drops the matching number by exactly one, which is what makes the induction proof of König work. Hall's violating set is the same set the König construction already produces. Regularity gives Hall's condition by counting edges out of a set two ways, and that is the most reused argument in this unit. The defect version pads with dummy vertices and then subtracts them off. The 2 factor theorem converts a non bipartite problem into a bipartite one by splitting each vertex into an in copy and an out copy, a trick that comes back with network flows.

## Still unclear

- The 2 factor argument assumes the edges lie in one non trivial component so that an Euler circuit exists. For a disconnected graph, apply it per component. Worth confirming the lecture said this.
- Whether the 2 factor theorem extends to multigraphs. The Euler argument seems not to care.
