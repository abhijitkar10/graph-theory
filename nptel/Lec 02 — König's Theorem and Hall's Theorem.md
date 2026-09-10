---
tags: [academics, graph-theory, nptel, lecture]
lecture: 2
unit: Covering Problems
source: NPTEL Graph Theory (Dr. L. Sunil Chandran, IISc), Lecture 02
---

# Lec 02 — Matchings, König's theorem and Hall's theorem

Previous: [[Lec 01 — Vertex Cover and Independent Set]] · Index: [[NPTEL Index]] · Next: [[Lec 03 — More on Hall's Theorem and Applications]]

Covered here: alternating and augmenting paths, Berge's theorem, König's min-max theorem for bipartite graphs, Hall's marriage theorem, and how the last two imply each other.

These are my own written up versions of the mathematics rather than a transcript. Where a proof can go several ways I give the cleanest standard route and mention the alternatives.

## How much this matters

Overall this note is core, and it is the single most useful of the NPTEL notes.

Know cold: [[Lec 02 — König's Theorem and Hall's Theorem#Berge's theorem|Berge]] and [[Lec 02 — König's Theorem and Hall's Theorem#Hall's theorem|Hall's statement with its easy direction]].

Know the construction: [[Lec 02 — König's Theorem and Hall's Theorem#König's theorem|König by alternating reachability]]. This is the fullest write up of that construction anywhere in the vault, so use it if the version in [[2026-07-29 Matchings 2 — Berge and König]] moves too fast.

Know the idea: [[Lec 02 — König's Theorem and Hall's Theorem#The sufficiency direction, by induction|Hall by induction]], in particular why the tight set has to be dealt with first.

Read once: [[Lec 02 — König's Theorem and Hall's Theorem#König and Hall imply each other|the equivalence of König and Hall]]. Worth seeing once, but you will not be asked to reproduce both directions.

## Notation

G = (A ∪ B, E) is a bipartite graph with the two sides A and B, and every edge joins A to B. M is a matching, meaning a set of pairwise disjoint edges. As in [[Lec 01 — Vertex Cover and Independent Set]], α′(G) is the matching number and β(G) the vertex cover number. For a set S of vertices, N(S) is the set of all vertices adjacent to something in S.

A vertex is M saturated, or matched, when it is an endpoint of some edge of M, and free otherwise. The symmetric difference of two matchings is the set of edges lying in exactly one of them.

Recall from [[2026-07-24 Preliminaries]] that bipartite means the vertices split into two independent sets, and equivalently that there are no odd cycles. That absence of odd cycles is the hidden engine of everything below.

## Alternating and augmenting paths

Fix a matching M.

An M alternating path is a path whose edges alternate between being in M and not being in M.

An M augmenting path is an alternating path whose two endpoints are both unmatched.

```
 unmatched            unmatched
    u  ---- v ==== w ---- x        ---- means not in M
                                   ==== means in M
```

The word augmenting is earned by the flip. Such a path starts and ends with non matching edges, so along a path with 2k+1 edges it carries k+1 non matching edges and k matching ones. Swap them, taking the non matching edges in and throwing the matching edges out.

```
 before:  u ---- v ==== w ---- x        one M edge here
 after:   u ==== v ---- w ==== x        two M edges, one gained
```

The result is still a matching, since each interior vertex simply swaps one partner for another and the two endpoints were unmatched so nothing clashes, and it has exactly one more edge.

So an augmenting path is a certificate that your matching is not maximum. Berge's theorem says that is the only obstruction.

## Berge's theorem

Theorem (Berge). A matching M is maximum exactly when no M augmenting path exists.

Given: a matching M.
To show: the two conditions are equivalent.

One direction is the flip above read backwards. If an augmenting path existed, the flip would produce a strictly larger matching, so M would not be maximum.

For the other direction, suppose M is not maximum, so some matching M′ has more edges. Let H be the symmetric difference of M and M′.

The structural fact is that every vertex touches at most one edge of M and at most one of M′, so every degree in H is at most 2. A graph of maximum degree 2 is a disjoint union of paths and cycles. Along any of them the edges must alternate between M and M′, since two consecutive edges from the same matching would share a vertex, which matchings forbid.

Now count. Since M′ has more edges than M, some component of H contains more M′ edges than M edges. A cycle alternates, so it is even and holds equally many of each. A path with an even number of edges starts and ends with different types, so again equal. Only a path with an odd number of edges can carry a surplus, and it carries one extra of whichever type sits at both of its ends.

So the surplus component is an odd path beginning and ending with M′ edges. Call it P. Its two endpoints are unmatched by M, because the end edge belongs to M′ and not to M, and if the endpoint had an M edge then that edge would have continued the path inside H. So P is an M augmenting path, contradicting the assumption that none existed.

This is the workhorse of the whole unit, because it converts "is my matching biggest" into "can I find an augmenting path", which is a search you can actually run. Hopcroft and Karp, the Hungarian algorithm and Edmonds' blossom algorithm are all built on hunting augmenting paths.

## König's theorem

Theorem (König, 1931). In a bipartite graph, α′(G) = β(G), so the maximum matching and the minimum vertex cover have the same size.

Given: G is bipartite.
To show: the two numbers are equal.

We already know α′ ≤ β in every graph, from [[Lec 01 — Vertex Cover and Independent Set]], so the whole job is to build a vertex cover of size exactly α′.

Let M be a maximum matching and let U be the set of vertices in A not matched by M. Let Z be the set of all vertices reachable from U by M alternating paths, meaning paths starting at U whose first edge is not in M and which alternate from there. Split Z into S, the part in A, and T, the part in B. Note that U sits inside S, since each unmatched vertex reaches itself by the empty path.

The claim is that K, defined as everything in A outside S together with all of T, is a vertex cover of size at most the size of M. Four steps prove it.

First, every vertex of T is matched, and its partner lies in S. If some t in T were unmatched, the alternating path from U to t would start and end at unmatched vertices, making it an M augmenting path, which by Berge contradicts M being maximum. So t is matched, say to a vertex a in A. Extend the alternating path reaching t by the matching edge ta, which keeps it alternating, so a lies in S.

Second, no edge joins S to the part of B outside T. Suppose s is in S, b is outside T, and sb is an edge. Take the alternating path reaching s. It arrives at s either along a matching edge or not at all, in the case where s is in U, because by the first step any alternating path entering A from B does so along an M edge. In either case appending the non matching edge sb keeps the path alternating, which would put b in T after all.

Third, K is a vertex cover. Take any edge ab with a in A and b in B. If a is not in S then a lies in the part of A outside S, which is inside K. If a is in S then by the second step b must be in T, which is also inside K. Either way the edge is covered.

Fourth, K is no bigger than M. Every vertex of A outside S is matched, since the unmatched vertices of A are exactly U, which sits inside S. Every vertex of T is matched, by the first step. So each vertex of K sits on its own M edge. Two vertices of K cannot share the same M edge, because that would need an M edge running from the part of A outside S to T, and by the first step every vertex of T is matched into S rather than into that part. So the M edges are distinct and K has at most as many vertices as M has edges.

Therefore β is at most the size of K, which is at most α′, and combined with α′ ≤ β the two are equal.

Check it on the path a–b–c–d, which is bipartite with A = {a, c} and B = {b, d}.

```
 a ——— b ——— c ——— d
```

Here α′ = 2, from the edges ab and cd, and β = 2, from the cover {b, c}. Equal, as promised. On the triangle, which is not bipartite, α′ = 1 and β = 2, which shows bipartiteness is genuinely needed.

König also follows from Hall, as shown below, from the max-flow min-cut theorem by treating the bipartite graph as a unit capacity network, in Lecture 31, and from Dilworth's theorem, in Lecture 08. All four are essentially the same theorem in different clothing.

## Hall's theorem

Theorem (Hall, 1935). Let G be bipartite with sides A and B. There is a matching saturating every vertex of A exactly when the size of N(S) is at least the size of S for every subset S of A.

That condition is called Hall's condition. In the marriage phrasing, A is a set of people, B the possible partners, and edges mean willingness. Everyone in A can be matched exactly when no group of k people collectively knows fewer than k candidates.

### The necessary direction

Suppose a matching saturates A, and take any subset S. Each vertex of S has its own partner, all of those partners lie in N(S), and they are distinct because it is a matching. So N(S) contains at least as many vertices as S.

### The sufficiency direction, by induction

Induct on the size of A.

For the base case, with one vertex, Hall's condition applied to A itself gives N(A) at least one vertex, so the single vertex has a neighbour and you match them.

For the step, assume the theorem for every smaller left side and split on how tight Hall's condition is.

Case one, slack everywhere, meaning the size of N(S) is at least the size of S plus one for every non empty proper subset S of A. Pick any vertex a in A and any neighbour b, which exists because N({a}) is non empty. Match a to b and delete both. Hall's condition survives in what remains, because for any subset S of the rest, deleting b removes at most one vertex from its neighbourhood, so the neighbourhood still has at least the size of S. By induction the rest of A can be matched, and adding the edge ab finishes it.

Case two, some tight set, meaning some non empty proper subset S of A has N(S) exactly the size of S. That set uses up its neighbourhood exactly, so it has to be handled separately before anything else.

First, Hall's condition holds inside the subgraph on S together with N(S), because for a subset of S the neighbourhood is the same there as in G. Since S is smaller than A, induction gives a matching saturating S, which uses up all of N(S).

Second, let G′ be what remains, with sides A minus S and B minus N(S). Check Hall's condition there. Take a subset T of A minus S and apply Hall's condition in G to S together with T, which gives that N(S ∪ T) has at least the size of S plus the size of T. But N(S ∪ T) is N(S) together with N(T), and N(S) has exactly the size of S, so the part of N(T) lying outside N(S) must supply the remaining amount, which is at least the size of T. That is exactly Hall's condition in G′. Since A minus S is smaller than A, induction matches it inside G′.

Third, the two matchings use disjoint vertices, since the first lives inside S together with N(S) and the second avoids both. Their union saturates A.

A failure worth looking at. Take A with three vertices, B with two, and every vertex of A joined to both vertices of B. Taking S to be all of A gives N(S) of size 2 against S of size 3, so Hall's condition fails, and indeed three people cannot be matched to two partners.

## König and Hall imply each other

Each is a two line consequence of the other.

From Hall to König. Let K be a minimum vertex cover. Write P for the part of K lying in A and Q for the part lying in B, so K is P together with Q. Consider the bipartite subgraph between the vertices of A outside P and the set Q. Hall's condition holds there, because if some subset had too few neighbours you could swap those neighbours into the cover in place of the subset, replacing part of K by something strictly smaller that still covers everything, contradicting minimality. So that subgraph has a matching saturating the vertices of A outside P, and symmetrically there is one saturating P on the other side. Assembling them gives a matching of size equal to the size of K, so α′ ≥ β, and with α′ ≤ β this gives equality.

From König to Hall. Suppose Hall's condition holds and no matching saturates A. Then α′ is smaller than the size of A, so by König β is too. Take a minimum cover K and let S be the part of A outside K. Every edge leaving S must be covered on the B side, so N(S) sits inside the part of K lying in B. Counting, the size of N(S) is at most β minus the number of cover vertices in A, while the size of S is the size of A minus that same quantity. Since β is below the size of A, subtracting the same amount from both keeps the inequality, and N(S) comes out strictly smaller than S, violating Hall's condition.

The moral is that König is the min-max form, saying the largest packing equals the smallest cover, and Hall is the feasibility form, saying exactly when a perfect assignment exists. Min-max theorems and feasibility criteria are usually two faces of one result, a pattern you meet again with Menger in Lecture 10 and max-flow min-cut in Lecture 31.

## What to remember

An augmenting path is a proof that your matching is not maximum, and flipping it gains exactly one edge. Berge says that is the only obstruction, which turns optimality into a searchable condition and underlies every matching algorithm. The symmetric difference of two matchings always splits into alternating paths and cycles, and maximum degree 2 is all you need for that, a trick that reappears constantly. König says a bipartite graph has α′ = β, and the proof constructs the cover from alternating reachability out of the unmatched vertices. Hall says matching all of A is possible exactly when no set of A vertices is starved of neighbours, proved by induction and splitting on whether some set is tight. The tight set case is the heart of Hall's proof, because a set with no spare neighbours has to be disposed of first before you recurse on what is left. And König, Hall, Menger, max-flow min-cut and Dilworth are all the same theorem in different disguises.

## Still unclear

- I proved König via alternating reachability. Chandran may instead derive it from Hall, or defer it to max-flow min-cut. Worth checking which route the lecture takes.
- The Hall to König direction above is stated compactly and could be expanded if the full detail is ever needed.
- The Hopcroft and Karp running time is mentioned but not proved.
