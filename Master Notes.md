---
tags: [academics, graph-theory, master, moc]
type: master
---

# Master Notes, graph theory by concept level

Hub: [[Graph Theory]] · Cram version: [[Revision Sheet]] · Shortest version: [[Bare Minimum]]

Every definition, lemma, claim and exercise from all my notes, reorganised by what depends on what rather than by the date it was taught. The class notes follow the timeline. This file follows the logic.

Where the class jumped over something, this file fills the gap with a short section labelled BRIDGE. Those are concepts used but never defined anywhere else in my notes.

To study with it, work down one level at a time and do not start a level until the one before it feels solid, because each level genuinely uses the previous one.

## Dependency map

```
 L0  Vocabulary ──────────────┐
      │                       │
 L1  Walks, paths, distance   │
      │           │           │
 L2  EXTREMAL     └──► L3  Counting and density
      METHOD               │
      │  │                 │
      │  └──► L4  Trees ◄──┘
      │           │
      │      L5  Bipartite
      │           │
      ├──────► L6  Euler traversal
      │           │
      └──────► L7  Covering and packing (matchings)
                  │
              L8  Connectivity ──► L9  Planarity
                  │
              L10 The road ahead
```

Read the arrows as "you need this first". The two spines of the subject are Level 2, the extremal method, and Level 3, counting. Nearly every proof past that point is one of those two dressed up.

| Level | Title | Where it stands |
|---|---|---|
| 0 | Vocabulary, what a graph even is | solid |
| 1 | Walking around a graph | solid |
| 2 | The extremal method | solid, and it is the key technique |
| 3 | Counting and density arguments | solid |
| 4 | Trees | solid |
| 5 | Bipartite graphs | solid |
| 6 | Traversal, Euler circuits | solid |
| 7 | Covering and packing, matchings | solid through Tutte |
| 8 | Connectivity | solid, through Menger, fans and cycles through k vertices |
| 9 | Planarity | touched once |
| 10 | The road ahead | not started |

# Level 0, vocabulary

Prerequisites: none. This level exists because almost every mistake I have made so far has been a definition mistake rather than a proof mistake.

A simple graph has no self loops and no repeated edges, which gives the fact used constantly that a vertex is never its own neighbour. Writing u ~ v means u is adjacent to v. The neighbourhood N(v) is the set of vertices adjacent to v, and for a set S, N(S) means the vertices outside S with a neighbour in S. The closed neighbourhood N[v] is N(v) together with v itself. The degree deg(v) counts the edges touching v, and n and m count vertices and edges.

A clique is a set of pairwise adjacent vertices, so a Kᵣ sitting inside G. An independent set is a set with no edges inside it. The complement of G has the same vertices with edges exactly where G has none, so an independent set in G is a clique in the complement.

For degrees, δ(G) is the minimum and Δ(G) the maximum. My problem sheets sometimes write D(G) for δ(G), which is the same thing. The average degree is 2m/n, and the edge density ε(G) is m/n, which is half the average degree. A graph is k regular when every degree is exactly k.

Sources: [[2026-07-24 Preliminaries]], [[Lec 01 — Vertex Cover and Independent Set]], [[Lec 02 — König's Theorem and Hall's Theorem]], [[Assignment 1]].

## BRIDGE 0.1, subgraph, induced subgraph, spanning subgraph

This is used everywhere, in phrases like induced path, induced P₃, and a subgraph with δ(H) ≥ k, but it is never actually defined in my notes.

H is a subgraph of G when its vertices are among G's vertices and its edges among G's edges. You may delete vertices and edges freely.

The induced subgraph G[S] takes a vertex set S and keeps every edge of G with both ends in S. You delete vertices, but you are not allowed to drop edges among the survivors.

A spanning subgraph keeps every vertex and deletes only edges.

```
   G:  a———b        G[{a,b,c}] induced:  a———b      a subgraph, not induced:
       | \ |                             |   |            a———b
       c———d                             c———             |
                                    edge ac is forced      c
```

The distinction earns its keep in three places. An induced path, as in Q3 and Q5 of [[Tutorial 1]], means the path has no chords, so a–b–c is induced only when the edge ac is absent from G. The greedy deletion theorem of Level 3 produces an induced subgraph, since it deletes whole vertices and never individual edges. And spanning is the right word for a spanning tree, which keeps every vertex.

The rule of thumb is that induced means you do not get to choose which edges to ignore, which is what makes statements about induced subgraphs stronger and harder.

# Level 1, walking around a graph

Prerequisites: Level 0. This level exists because four near identical words mean different things, and getting them wrong wrecks the Euler material.

| Term | Repeats vertices | Repeats edges |
|---|---|---|
| walk | allowed | allowed |
| trail | allowed | forbidden |
| path | forbidden | forbidden |
| circuit | allowed | forbidden, and closed |

Length always means the number of edges, so a path on m vertices has length m−1. This trips me up constantly.

A component is a maximal connected subgraph, and a trivial component is a single isolated vertex with no edges. Components partition the vertex set, so every vertex lies in exactly one.

For distances, d(u,v) is the length of a shortest u to v path. The eccentricity of v is the distance to the vertex furthest from it, and the radius and diameter are the minimum and maximum of the eccentricities. The girth is the length of the shortest cycle and the circumference the length of the longest.

Five results live here. Radius and diameter satisfy rad ≤ diam ≤ 2·rad, proved by routing everything through a centre. Distance layers Dₙ = {v : d(v₀,v) = n} have the property that no edge skips a layer. A shortest path has no chords, so shortest paths are induced. A connected graph that is not complete contains an induced path on three vertices. And girth ≤ 2·diam + 1, tight at odd cycles.

Sources: [[Assignment 1]] Q4, Q5, Q6, Q11, and [[Tutorial 1]] Q3, Q5.

## BRIDGE 1.1, every walk contains a path

Used silently in [[Assignment 1]] Q11 to prove transitivity. Worth stating properly, because it is the reason you can be sloppy about walks versus paths whenever you only care about reachability.

Lemma. If there is a u to v walk, then there is a u to v path.

Take a u to v walk W with the fewest edges, which is an extremal choice, Level 2 in miniature. Suppose W repeats a vertex x, visiting it at two different times. Cut out the entire loop between those two visits. What remains is still a u to v walk, since you leave x and re-enter the route at x, and it is strictly shorter, contradicting minimality. So W repeats no vertex, which is to say W is a path.

The payoff is that "u and v lie in the same component" can be checked with any walk, however messy. You never have to be careful about repeats when the only question is whether you can get there.

# Level 2, the extremal method

Prerequisites: Levels 0 and 1. This is the single most important technique in the course so far, and nine separate results below are the same idea.

The method is to choose an object that is extreme in some way, meaning longest, maximal, minimal, largest index or rightmost endpoint, and then ask what the fact that it cannot be improved forces to be true. The answer is usually the whole proof.

## Maximal versus longest, get this straight first

Maximal means it cannot be extended. Longest, or maximum, means no longer one exists anywhere in the graph. Finding a maximal object is greedy, since you walk until you get stuck, and it takes polynomial time. Finding a longest path is NP complete.

Every proof below only needs the property that the object cannot be extended, so maximal always suffices. That is a much cheaper object, and one always exists. Source: [[2026-07-24 Preliminaries]].

## The trapped endpoint principle

Take a maximal path P. Both of its endpoints are trapped, meaning every one of their neighbours already lies on P, because an outside neighbour could be tacked on.

This applies only to the endpoints. Interior vertices are free to have neighbours anywhere, because you can only extend a path at its ends. See Claim 1 of [[2026-07-24 Long Path Theorem]].

## What falls out of it

| Result | Statement | Source |
|---|---|---|
| Lemma A | δ ≥ k gives a path on at least k+1 vertices | [[2026-07-24 Preliminaries]] |
| Lemma B | δ ≥ 2 gives a cycle | [[2026-07-24 Preliminaries]] |
| Lemma C | δ ≥ k gives a cycle of length at least k+1 | [[2026-07-24 Preliminaries]] |
| Even cycle | δ ≥ 3 gives an even cycle | [[2026-07-24 Preliminaries]] |
| Long path theorem | connected gives a path of length at least min{2δ, n−1} | [[2026-07-24 Long Path Theorem]] |
| Path or cycle | connected gives a path or cycle of length at least min{2δ, n} | [[Assignment 1]] Q9 |
| Two longest paths meet | any two longest paths share a vertex | [[Tutorial 1]] Q4 |
| Maximal trail gives Euler | a maximal trail is closed and uses every edge | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] |
| Greedy deletion | strip low degree vertices until stuck | [[2026-07-24 Preliminaries]] |
| Helly in one dimension | take the largest left endpoint | [[Tutorial 1]] Q6 |
| Walk contains a path | take the shortest walk | Bridge 1.1 above |

## The supporting moves

These small tools show up inside extremal proofs. Pigeonhole says two sets inside a box of size k whose sizes add past k must overlap. Folding a path into a cycle uses two crossing edges, offset by one, to close the loop. Snip and extend reopens a cycle to free an endpoint you can grow. Shortest forbids shortcuts says a chord would contradict minimality. An exchange argument modifies any optimum to agree with your greedy choice without losing size. Superimposing two matchings gives a graph of maximum degree 2, which splits into paths and cycles. And parity says odd plus odd is even, so three quantities cannot all be odd.

Sources: [[2026-07-24 Long Path Theorem]] Claims 3, 4 and 6, [[Tutorial 1]] Q3 and Q5, [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]], [[Lec 02 — König's Theorem and Hall's Theorem]], [[2026-07-24 Preliminaries]].

# Level 3, counting and density

Prerequisites: Levels 0 and 1. This level is independent of Level 2 and forms a second spine. When extremality does not crack a problem, count something two ways.

## The handshake lemma

The degrees sum to 2m, proved by counting pairs of a vertex and an edge touching it in two ways. Source: [[2026-07-24 Preliminaries]].

## BRIDGE 3.1, the parity corollary of handshake

Never stated in my notes, but it is the cleanest way to see why Euler's theorem looks the way it does.

Corollary. In every graph the number of vertices of odd degree is even.

Split the handshake sum by parity. The even degree vertices contribute a sum of even numbers, which is even, and the whole sum is 2m, which is even. Subtracting, the contribution of the odd degree vertices is even. But that is a sum of odd numbers, and a sum of odd numbers is even exactly when there is an even count of them.

Check it on small graphs. A path a–b–c has degrees 1, 2, 1, so two odd vertices. A triangle has degrees 2, 2, 2, so none. You can never build a graph with exactly one vertex of odd degree.

This bridges to Euler because [[2026-07-27 Euler Circuits]] shows an Euler circuit needs every degree even, and the corollary answers the next question. An Euler trail, open with different start and end, needs exactly two odd vertices, and by the corollary you can never have just one. That is why the theory splits into zero odd vertices giving a circuit and two odd vertices giving an open trail, with no other possibility. Königsberg has four odd vertices, which kills both.

## Density results

Edge density ε(G) is m/n, which is half the average degree, so the two are the same fact.

If m exceeds (n−1)(n−2)/2 then G is connected, and the bound is sharp, since Kₙ₋₁ plus an isolated vertex sits exactly at the threshold.

Density k forces a subgraph with minimum degree at least k, by greedy deletion, where the density rises as you strip. If m exceeds k(n−1) then a (k+1) edge connected subgraph exists, by a minimal subgraph argument.

For the smallest constant b(k) such that m ≥ kn + b(k) forces a k connected subgraph, the bounds are −k(k+1)/2 ≤ b(k) ≤ −k, exact at b(1) = −1.

Sources: [[2026-07-24 Preliminaries]], [[Assignment 1]] Q16 and Q18.

## BRIDGE 3.2, that greedy deletion theorem has a name

Degeneracy is on my syllabus as its own topic, and I have already proved the main fact without knowing the name.

A graph is d degenerate when every subgraph of it has a vertex of degree at most d, and the degeneracy is the smallest such d.

The link is that [[2026-07-24 Preliminaries]] proves that if every subgraph failed to have a low degree vertex you could strip forever. Restated, G is d degenerate exactly when the greedy procedure of repeatedly deleting a vertex of degree at most d empties the graph.

That procedure produces a degeneracy ordering, the reverse of the deletion order, in which every vertex has at most d neighbours earlier than itself.

Feeding a degeneracy ordering to greedy colouring gives χ(G) ≤ degeneracy(G) + 1, since each vertex sees at most d already coloured neighbours. Every tree is 1 degenerate, because every subgraph has a leaf, so χ ≤ 2, which is right since trees are bipartite. Every planar graph is 5 degenerate, which gives the six colour theorem for free.

So Level 3's greedy deletion, the syllabus topic of degeneracy, and greedy colouring are one idea seen three times.

## Girth forces room

All of these are the same count. Take {v}, then N(v), then the outer neighbours, forced disjoint by the absence of short cycles.

Girth at least 5 gives δ ≤ √(n−1), which fixes n and caps the degree. A k regular graph of girth 5 needs at least k²+1 vertices, which fixes the degree and forces the size up, and is tight at the Petersen graph and at C₅. The Moore bound generalises this to arbitrary girth. A graph of diameter k and minimum degree d has roughly kd/3 vertices, found by grabbing every third vertex of a shortest path so their neighbourhoods stay disjoint.

The shared engine is that large girth means balls around a vertex are trees, with no shortcuts, so each level multiplies by d−1. Small girth is exactly what lets a graph be both small and dense.

Sources: [[Assignment 1]] Q7, Q8, Q10, and [[Tutorial 1]] Q2.

# Level 4, trees

Prerequisites: Levels 0 to 3, since Lemma B from Level 2 is used to prove that leaves exist. Trees are the boundary case between too few edges to connect and enough edges to make a cycle, and that tension is where all their properties come from.

A tree is a connected acyclic graph. A forest is any acyclic graph, so a disjoint union of trees.

## The four characterisations

Four conditions are equivalent: connected and acyclic, any two vertices joined by a unique path, minimally connected so that removing any edge disconnects, and maximally acyclic so that adding any edge creates a cycle. This is Theorem 1.5.1 in Diestel, worked in [[Assignment 1]] Q19.

The picture is that a tree is exactly the tipping point. Take an edge away and it falls apart, put one in and a cycle appears. Unique paths is the same balance seen from the middle.

## Core facts

Every tree on at least two vertices has a leaf, since otherwise δ ≥ 2 and Lemma B produces a cycle. A tree on n vertices has exactly n−1 edges, by induction after deleting a leaf, and a forest with c components has n − c edges. Two distinct paths between the same pair would create a cycle, which gives unique paths.

A tree has at least Δ(T) leaves, found by deleting a vertex of maximum degree so that each of the Δ resulting pieces yields a leaf. If a tree has no vertex of degree 2 then the number of leaves is at least the number of internal vertices plus 2, which is pure handshake with no induction. The forest exchange property says that if a forest F has fewer edges than a forest F′ then some edge of F′ extends F, because F has more components. Tree order, where x ≤ y when x lies on the path from the root to y, is a partial order.

For maximum independent sets in a tree, splitting by level fails, since the larger of the odd and even levels is not in general the answer. Two correct methods exist. Greedy takes all the leaves, deletes their parents and recurses, justified by an exchange argument. Dynamic programming sets MIS(v,0) as the sum over children of max{MIS(u,0), MIS(u,1)} and MIS(v,1) as 1 plus the sum of MIS(u,0), and runs in linear time.

For matchings in a tree, a leaf's parent lies in every maximum matching, and the matching number ranges anywhere from 1 for a star to ⌊n/2⌋, with no formula in terms of depth.

Trees connect outward in two ways. They are 1 degenerate, by Bridge 3.2, and bipartite, by colouring on level parity. The forest exchange property is the matroid exchange axiom, which is why Kruskal's algorithm works.

Sources: [[2026-07-24 Preliminaries]], [[Assignment 1]] Q19 to Q23, [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]], [[2026-08-10 Matchings in Bipartite Graphs]].

# Level 5, bipartite graphs

Prerequisites: Levels 0 to 2 for the even cycle machinery, and Level 4 for the tree example. Bipartiteness is the single hypothesis that turns several NP-hard problems polynomial, so knowing exactly what it means is worth a lot later.

A graph is bipartite when its vertex set splits into two independent sets X and Y, so that every edge crosses and none lies inside a part. Equivalently, it can be 2 coloured with no edge joining two vertices of the same colour.

## The characterisation

A graph is bipartite exactly when it has no odd cycle.

For the forward direction, walking around a cycle alternates sides, so closing it up forces even length. For the converse, root each component and split the vertices by the parity of their distance from the root, and any edge inside a part would close an odd cycle.

In a connected bipartite graph the bipartition is unique up to swapping the names of the sides, because all paths from a fixed root to a given vertex have the same parity. Uniqueness needs connectedness, since each component can be flipped independently, so two disjoint edges admit four bipartitions.

The recurring trick is to colour by a parity: level parity for trees, distance parity here, and the parity of the number of ones for the hypercube.

Sources: [[2026-07-24 Preliminaries]], [[2026-07-29 Matchings 2 — Berge and König]].

## The hypercube as a worked family

| Invariant | Value |
|---|---|
| vertices | 2ⁿ |
| degree | n, so it is n regular |
| edges | n·2ⁿ⁻¹ |
| diameter | n, which is the Hamming distance |
| girth | 4, for n ≥ 2 |
| circumference | 2ⁿ, so it is Hamiltonian |
| bipartite | yes, by the parity of the number of ones |
| planar | Q₃ yes, exactly at the limit, Q₄ no |

Sources: [[Tutorial 1]] Q1 and [[Assignment 1]] Q2.

## What needs bipartiteness

König, that α′ = β. Hall's matching criterion. The fact that k regular bipartite graphs have a perfect matching and split into k of them. The edge colouring result that bipartite graphs need exactly Δ colours and never Δ+1. And the planarity bound m ≤ 2n−4, which is stronger than 3n−6.

# Level 6, traversal and Euler circuits

Prerequisites: Level 1, where the trail and path vocabulary is essential, Level 2 since both proofs are extremal or inductive, and Bridge 3.1 for the parity corollary.

An Euler circuit is a circuit containing every edge. In plain terms, draw the whole graph in one pen stroke without retracing, finishing where you started.

## Euler's theorem

A graph has an Euler circuit exactly when it has at most one non trivial component and every vertex has even degree.

The necessary direction, Lemma 1, holds because each visit burns exactly two edges, so the degrees pair up, and at the start vertex the first edge pairs with the last.

The sufficient direction, Lemma 2, has two proofs and both are worth knowing. By induction on the number of edges, pull out a cycle, which keeps every degree even, recurse on the components, and splice the pieces back in as detours. This is fiddly, because deleting a cycle can shatter the graph, so you recurse per component and glue. By the extremal method, take a maximal trail, which is cleaner because the graph is never split.

The extremal proof runs in two claims. First, a maximal trail is closed, because an open trail uses an odd number of edges at its final endpoint, two per pass through plus one for the last arrival, which clashes with even degree. Second, a maximal trail uses every edge, because being closed it can be restarted anywhere, so any leftover edge touching it would extend it.

Sources: [[2026-07-27 Euler Circuits]] and [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]].

## Using the theorem

To rule out an Euler circuit, negate the conjunction, which by De Morgan becomes a disjunction. More than one non trivial component, or a single vertex of odd degree, is enough. The disjunction is the practical form, since one odd vertex kills it. Königsberg has four, so the bridge tour is impossible.

Isolated vertices are harmless, because an Euler circuit owes a visit to edges rather than to vertices. That is why the condition says at most one non trivial component instead of connected.

## The contrast that matters

An Euler circuit covers every edge once and has an easy degree test, so the problem is fully solved. A Hamiltonian cycle covers every vertex once and deciding it is NP complete, with no efficient characterisation known. Two near mirror questions sitting on opposite sides of the tractability line.

# Level 7, covering and packing, matchings

Prerequisites: Levels 0 to 5. This is where the syllabus proper begins. Four parameters pair up into two identities, one inequality that bipartiteness turns into an equality, and a criterion, Hall, that generates a dozen applications.

## The four parameters

The course uses West's letters. α(G) is the independence number, which you maximise. β(G) is the vertex cover number, which you minimise. α′(G) is the matching number, which you maximise. β′(G) is the edge cover number, which you minimise. So α means packing and β means covering, unprimed refers to vertices and primed to edges. Some books write ν for α′ and τ for β.

```
            packing (max)      covering (min)
 vertices     α                  β            α + β = n
 edges        α′                 β′           α′ + β′ = n
```

## The identities and the inequality

A set S is independent exactly when its complement is a vertex cover, which is one set with two names. That gives the first Gallai identity, α + β = n. The second, α′ + β′ = n, needs no isolated vertices. Also α(G) equals the clique number of the complement.

The inequality α′ ≤ β holds because matching edges are disjoint, so each needs its own cover vertex. Separately α′ ≤ ⌊n/2⌋, since a matching uses 2α′ distinct vertices. And β ≤ 2α′, because taking both endpoints of a maximum matching gives a set that covers everything.

Together these give the sandwich α′ ≤ β ≤ 2α′. The lower half is tight for every bipartite graph, by König, and the upper half is tight at the triangle and at disjoint triangles. The upper half is the standard 2 approximation for the NP-hard vertex cover problem.

Values worth memorising, where β = n − α throughout by Gallai:

| Graph | α′ | α | β = n−α | is α′ = β |
|---|---|---|---|---|
| Pₙ | ⌊n/2⌋ | ⌈n/2⌉ | ⌊n/2⌋ | yes |
| Cₙ | ⌊n/2⌋ | ⌊n/2⌋ | ⌈n/2⌉ | yes when even, no when odd |
| star Sₙ | 1 | n−1 | 1 | yes |
| Kₙ | ⌊n/2⌋ | 1 | n−1 | no, for n ≥ 3 |
| tree | k | n−k | k | yes |
| K(k,l) | min(k,l) | max(k,l) | min(k,l) | yes |

The last column holds exactly for the bipartite entries, and that pattern is König. The triangle is the minimal witness of α′ < β, with 1 against 2, and it is also the smallest odd cycle, which is exactly why König needs bipartiteness.

Sources: [[Lec 01 — Vertex Cover and Independent Set]], [[2026-07-29 Matchings 2 — Berge and König]], [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]].

## Augmenting paths

An M alternating path has edges alternating in and out of M. An M augmenting path is alternating with both endpoints unmatched, which forces odd length.

Berge's theorem says M is maximum exactly when no M augmenting path exists. The engine of the hard direction is that the union of two matchings has maximum degree 2, so it splits into alternating paths and even cycles, and only an odd path can carry a surplus.

The algorithm follows. While an augmenting path exists, swap along it. It halts in at most ⌊n/2⌋ rounds. Berge is what makes the halting condition correct, which is why it matters: it turns "is this optimal" into a search, and every matching algorithm hunts augmenting paths.

A related exchange argument shows a leaf's edge lies in some maximum matching.

Sources: [[Lec 02 — König's Theorem and Hall's Theorem]] and [[2026-07-29 Matchings 2 — Berge and König]].

## The main theorems

| Result | Statement | Source |
|---|---|---|
| König | bipartite gives α′ = β | [[Lec 02 — König's Theorem and Hall's Theorem]] · [[2026-07-29 Matchings 2 — Berge and König]] |
| The smaller side | min of the two side sizes is only an upper bound on β, with equality needing complete bipartite | [[2026-07-29 Matchings 2 — Berge and König]] |
| Hall | a matching saturates A exactly when \|N(S)\| ≥ \|S\| for every S inside A | [[Lec 02 — König's Theorem and Hall's Theorem]] |
| König and Hall are equivalent | each is a two line consequence of the other | [[Lec 02 — König's Theorem and Hall's Theorem]] |
| Defect Hall | α′ = \|A\| minus the largest deficiency | [[Lec 03 — More on Hall's Theorem and Applications]] |
| A vertex in every maximum matching | every bipartite graph with an edge has one | [[2026-08-10 Matchings in Bipartite Graphs]] |
| At least β such vertices | peel one off and induct through König | [[2026-08-10 Matchings in Bipartite Graphs]] |
| König by induction | peel off that vertex and recurse, the shortest of the three proofs | [[2026-08-10 König by Induction, Hall, and Factors]] |
| k factor | spanning subgraph with every degree k, so a 1 factor is a perfect matching | [[2026-08-10 König by Induction, Hall, and Factors]] |
| 2k regular gives a 2 factor | Euler circuit, orient, split each vertex in two, apply Hall | [[2026-08-10 König by Induction, Hall, and Factors]] |
| Bad set | \|S\| < odd(G−S) certifies that no perfect matching exists | [[2026-08-19 Tutte's 1-Factor Theorem]] |
| Tutte's 1-factor theorem | perfect matching exactly when \|S\| ≥ odd(G−S) for every S | [[2026-08-19 Tutte's 1-Factor Theorem]] |
| Petersen, 1891 | every bridgeless cubic graph has a 1 factor | [[2026-08-19 Tutte's 1-Factor Theorem]] |

Four observations tie these together.

Petersen's proof works because in a cubic graph every odd component costs three edges to attach, odd by parity and at least 3 because 1 would be a bridge, while every vertex of S can pay exactly three. The threes cancel and Tutte's inequality drops out. Bridgelessness is the whole hypothesis, since a hub joined by three bridges to three odd blobs is cubic and of even order yet has no perfect matching.

The jump from bipartite to general graphs is a change of invariant. Hall's condition measures neighbourhood sizes, which is right only for bipartite graphs. For general graphs the obstruction is parity, since each odd component demands an exported vertex, and Tutte says that is the only obstruction. The canonical picture is triangles hanging off a small hub. Verified computationally: a hub of 2 with 5 triangles has odd(G−S) = 5 against |S| = 2, and no perfect matching.

One construction serves three theorems. The A₀, A₁, A₂, B₁, B₂ picture from König yields the minimum vertex cover for König, the Hall violating set A₀ ∪ A₁, and the shape of a Tutte bad set.

Odd cycles are the sole obstruction to a vertex lying in every maximum matching. That proof is valid for any graph right up to its final step, where it produces an odd cycle. An odd cycle is vertex transitive, so every vertex is missed by some maximum matching. Verified: C₃, C₅, C₇ and C₉ each have zero such vertices, while even cycles have all n.

Finally, hold on to the parity of the swap. Swapping along an odd alternating path gains an edge, which is Berge. Swapping along an even one preserves the size, which is exactly what makes the universal vertex proof work. The same operation serves opposite purposes.

## Applications of Hall

All follow one template. Build a bipartite graph in which the thing you want is a perfect matching, then verify Hall's condition, usually via regularity.

Every k regular bipartite graph has a perfect matching, by counting the edges out of a set in two directions. It follows that such a graph splits into k disjoint perfect matchings, since peeling one off leaves a regular graph. Systems of distinct representatives are Hall relabelled, with indices on one side and elements on the other. The Latin rectangle extension theorem works because the still free symbols form an (n−r) regular bipartite graph. Birkhoff and von Neumann's theorem, that a doubly stochastic matrix is a convex combination of permutation matrices, is the same idea again.

Source: [[Lec 03 — More on Hall's Theorem and Applications]].

## The complexity payoff

| Problem | General graphs | Bipartite graphs |
|---|---|---|
| maximum matching α′ | polynomial, by Edmonds | polynomial |
| minimum vertex cover β | NP-hard | polynomial, via König |
| maximum independent set α | NP-hard | polynomial, via α = n − β |

## BRIDGE 7.1, the min-max duality family

My notes keep saying these are all the same theorem without laying it out.

A min-max theorem says the largest packing equals the smallest blocker. Five results on my syllabus have that shape, and each implies the others.

| Theorem | Maximum thing | Minimum thing | Where |
|---|---|---|---|
| König | matching α′ | vertex cover β | Level 7, done |
| Hall | the feasibility form of König | | Level 7, done |
| Tutte | the feasibility form for general matchings | | Level 7, done |
| Menger | disjoint u to v paths | u to v separating set | Level 8, done |
| Max-flow min-cut | flow value | cut capacity | Level 10, ahead |
| Dilworth | antichain | chain cover | NPTEL Lec 08, ahead |

The pattern to carry is that every one of these has an easy direction, that max ≤ min, proved by blocking one item at a time, and a hard direction, equality, where you must construct an optimal blocker from an optimal packing. In König that construction was alternating reachability from the unmatched vertices. Menger's proof should do something structurally identical, and the question to ask when I get there is what plays the role of the alternating path.

The difference between the two shapes is worth naming. Hall and Tutte are feasibility statements, saying a perfect assignment exists exactly when some condition holds. König and Menger are min-max statements. They are two faces of one result, since the feasibility version is what you get by asking when the min-max quantity hits its ceiling.

# Level 8, connectivity

Prerequisites: Levels 0 to 4, and 7. Taught on 31 August in [[2026-08-31 Connectivity 1 — Minimum Degree and Whitney's Theorem]] and [[2026-08-31 Blocks, Ear Decomposition, and k-Connectivity]].

## The two numbers

The vertex connectivity κ(G) is the fewest vertices whose removal disconnects the graph, and the edge connectivity λ(G) is the fewest edges. The chain κ(G) ≤ λ(G) ≤ δ(G) always holds, since vertices are at least as powerful as edges, and killing one vertex's edges always disconnects it.

A graph is k-connected when no set of fewer than k vertices separates it, and, a clause easy to forget, when it has more than k vertices. Without that clause Kₙ would count as n-connected rather than (n−1)-connected.

The two numbers genuinely differ. Two cycles sharing a single vertex have κ = 1 and λ = 2, so it is 2-edge-connected without being 2-connected. That small graph is worth carrying, and it turns up again as the counterexample to the union lemma below.

Standard values: 1 and 1 for a path, 2 and 2 for a cycle, n−1 for Kₙ, min(m,n) for K(m,n), and n for Qₙ.

## Minimum degree against connectivity

If δ(G) ≥ (n−1)/2 then G is connected. The proof is one count: if x and y were non adjacent with no common neighbour, then {x}, N(x), {y} and N(y) would be four disjoint sets adding to at least n+1. The bound is sharp, since two disjoint copies of the complete graph on n/2 vertices have minimum degree (n−2)/2 and are disconnected.

Raising the hypothesis to δ ≥ n/2 buys much more. Every pair is then adjacent or shares a neighbour, and by Dirac's theorem the graph has a Hamiltonian cycle. Dirac's proof is the long path theorem of Level 2 with one extra step that drags every stray vertex onto the cycle, so learn it as a variation rather than as new material.

Minimum degree cannot force k-connectivity, as two huge cliques glued at one cut vertex shows. But density does force edge connected subgraphs, since m > k(n−1) gives a (k+1) edge connected subgraph. The lesson of those two together is that minimum degree is local while connectivity is global, so a local hypothesis can never force global connectivity of the whole graph, though it can force it on a subgraph. Passing to a subgraph is the move that rescues the idea.

## Whitney's theorem

A graph on at least three vertices is 2-connected exactly when every pair of vertices has two internally vertex disjoint paths between them.

The easy direction is one sentence: a single deleted vertex can lie on at most one of two internally disjoint paths, so the other survives. The hard direction inducts on the distance between the pair, takes the vertex v just before y on a shortest path, gets two paths to v from the induction hypothesis, and in the awkward case walks back from y and stops at the first vertex already used. Stopping at the first one is exactly what makes the assembled paths disjoint.

Everything 2-connectedness buys follows from it. Any two vertices lie on a common cycle, and so do a vertex and an edge, and two edges, and for any three vertices there is a pair of paths from one to the other two meeting only at the start. All four are the same trick: subdivide an edge to turn it into a vertex, or add a vertex joined to two targets to turn a pair into one, then apply Whitney and undo.

## Blocks

A block is a maximal connected subgraph with no cut vertex. That is not the same as a maximal 2-connected subgraph, because a bridge is a block and so is an isolated vertex, and neither is 2-connected.

Two blocks meet in at most one vertex, and any vertex lying in two blocks is a cut vertex. Building a graph with one node per block and one per cut vertex, joined by containment, gives the block graph, and for a connected G it is a tree. A cycle in it would let you route around every cut vertex on the cycle, merging those blocks into one and contradicting maximality.

The corollary that gets used: two vertices of a connected graph lie in a common block exactly when no single cut vertex separates them.

## Ear decomposition

Subdividing an edge never changes whether a graph is 2-connected, in either direction.

An ear of a subgraph H is a path whose two ends lie in H and whose interior does not. It is trivial when it is a single edge, open when its two ends differ, and closed when they coincide. An ear decomposition partitions the edges into E₁, a cycle, followed by ears of everything built so far, and it is open when every ear after the first is open.

Theorem. A graph on at least three vertices is 2-connected exactly when it has an open ear decomposition.

Openness is the whole point. A closed ear hangs on a single vertex, so deleting that one vertex would strand it, and the induction that proves 2-connectedness would fail at precisely that step.

## The k-connected version

The statement that G is k-connected exactly when every pair has k internally disjoint paths is true, and it is the global form of Menger's theorem, proved below. An induction on k does not get there, because knowing that l paths exist gives no grip on where an (l+1)-th would come from.

Three supporting facts are worth keeping anyway. A (l+1)-connected graph has δ ≥ l+1. A k-connected graph minus any edge is (k−1)-connected. And if H₁ and H₂ are l-connected and share at least l vertices, their union is l-connected. That last one fails without the sharing condition: two triangles glued at one vertex are each 2-connected and their union is not.

For k = 2 the local statement can be proved with what we have. If x and y are non adjacent and no single vertex separates them, they lie in a common block, that block is 2-connected, and Whitney inside it gives the two paths.

## Menger's theorem

The statement is that for non-adjacent x and y the least size of a separator equals the greatest number of internally disjoint x to y paths. The easy half is one separator vertex per path. The hard half is an induction on the number of vertices. Take a minimum separator S, let A be the side of x and B the rest, contract each side to a single vertex, apply the induction to both smaller graphs, and glue the paths at S. If every minimum separator is N(x) or N(y), either a vertex outside both neighbourhoods can be deleted, or the graph is x, y and their neighbourhoods and König's theorem finishes it. Every step is in [[2026-08-31 Menger's Theorem and Dirac's Fan Lemma#Menger's theorem, the induction|the Menger note]].

## Fans and what follows from Menger

The global form says G is k-connected exactly when every pair has k disjoint paths, and for an adjacent pair it uses the fact that deleting the edge leaves a (k−1)-connected graph. A fan from x to a set U is k paths from x sharing only x and ending at distinct vertices of U. Dirac's fan lemma says k-connected is the same as having a fan of size k from every x to every U of size at least k, provided there are more than k vertices. A consequence is that in a k-connected graph, any k vertices lie on a common cycle, by induction with a fan and a pigeonhole on arcs, and Kₖ,ₖ₊₁ shows k cannot be replaced by k + 1. See [[2026-08-31 Menger's Theorem and Dirac's Fan Lemma#The global form of Menger's theorem|the global form]], [[2026-08-31 Menger's Theorem and Dirac's Fan Lemma#Fans and Dirac's fan lemma|the fan lemma]] and [[2026-08-31 Menger's Theorem and Dirac's Fan Lemma#A cycle through any k vertices|the cycle theorem]].

Still ahead: edge connectivity and the structure of minimum cuts.

Sources: [[2026-08-31 Connectivity 1 — Minimum Degree and Whitney's Theorem]], [[2026-08-31 Blocks, Ear Decomposition, and k-Connectivity]], [[2026-08-31 Menger's Theorem and Dirac's Fan Lemma]], and [[Assignment 1]] Q12 to Q16.

# Level 9, planarity

Prerequisites: Levels 0 to 5. Touched exactly once, for Q₄, and it needs building out.

## BRIDGE 9.1, Euler's formula, which I used without proving

[[Tutorial 1]] Q1 uses the bound m ≤ 2n−4 and derives it from Euler's formula, but the formula itself was never justified.

Euler's formula says that for a connected plane graph, meaning one drawn with no crossings, with n vertices, m edges and f faces, n − m + f = 2.

The proof is induction on m. For the base, a tree has m = n−1 and only the outer face, so f = 1 and n − (n−1) + 1 = 2. For the step, if G is not a tree it has a cycle, so delete one cycle edge. That edge separated two distinct faces, which now merge, so m drops by one and f drops by one while n is unchanged, leaving n − m + f unchanged. Repeat until a tree remains.

Both counting bounds come from the same observation, that each face needs enough edges and each edge serves at most two faces. For a simple graph on at least three vertices every face has at least three edges, so 3f ≤ 2m, giving m ≤ 3n − 6. For a bipartite graph there are no triangles, so every face has at least four edges, so 4f ≤ 2m, giving m ≤ 2n − 4.

The bipartite derivation in full, since it is the one I actually needed: from 4f ≤ 2m we get f ≤ m/2, so 2 = n − m + f ≤ n − m/2, which rearranges to m ≤ 2n − 4.

| Graph | n | m | 3n−6 | 2n−4 | Planar |
|---|---|---|---|---|---|
| K₅ | 5 | 10 | 9 | | no, since 10 > 9 |
| K₃,₃ | 6 | 9 | 12 | 8 | no, since 9 > 8, and it needs the bipartite bound |
| Q₃ | 8 | 12 | 18 | 12 | yes, exactly at the limit |
| Q₄ | 16 | 32 | 42 | 28 | no, since 32 > 28 |

The trap to remember is that for Q₄ and K₃,₃ the general 3n−6 bound is too weak and says nothing at all, so you must use the bipartite bound. Checking bipartiteness first is the habit to build.

K₅ and K₃,₃ matter because Kuratowski's theorem, which is still ahead, says they are the only obstructions: a graph is planar exactly when it contains no subdivision of either.

Still ahead: Kuratowski's theorem, five colouring planar graphs, and the discharging method.

# Level 10, the road ahead

Everything on my syllabus not yet reached, in dependency order.

| Topic | Needs | NPTEL | Note |
|---|---|---|---|
| Edmonds' blossom algorithm | Tutte | Lec 04 to 06 | the algorithmic counterpart to Tutte's criterion |
| Tutte and Berge formula | Tutte | Lec 06 | maximum matching size in general graphs |
| Menger's theorem | Level 8, Bridge 7.1 | Lec 10 | done, in [[2026-08-31 Menger's Theorem and Dirac's Fan Lemma]] |
| Dirac's extensions | Menger | Lec 11 | done, fan lemma in the same note |
| Vertex colouring, greedy, degeneracy | Bridge 3.2 | Lec 13 to 14 | done, in [[2026-10-05 Coloring 1 — Greedy Colouring, Degeneracy, and Lower Bounds]]. χ ≤ Δ + 1 twice, χ ≤ k + 1 for k-degenerate graphs, χ ≥ ω and χ ≥ n over α |
| Brooks' theorem | greedy colouring | Lec 13 | |
| Edge colouring, König, Vizing | Level 7 | Lec 15 to 16 | the bipartite case is already done |
| Planar colouring | Level 9 | Lec 17 | |
| Perfect graphs | Levels 5 and 7 | Lec 23 to 27 | |
| Hamiltonian graphs | Level 6 contrast | Lec 28 to 30 | |
| Ramsey theory | Level 3 counting | Lec 36 | |
| Network flows and minimum cuts | Bridge 7.1 | Lec 31 to 34 | max-flow min-cut implies König |
| Discharging method | Level 9 | not in NPTEL | must come from West |

Tutte's theorem was on this list and is now done, in [[2026-08-19 Tutte's 1-Factor Theorem]]. So are 2-connected graphs and ear decomposition, in [[2026-08-31 Blocks, Ear Decomposition, and k-Connectivity]].

# Complete index of results

Every named claim, lemma and theorem across all my notes, alphabetically.

| Result | Level | Where |
|---|---|---|
| Berge's theorem | 7 | [[Lec 02 — König's Theorem and Hall's Theorem]] · [[2026-07-29 Matchings 2 — Berge and König]] |
| Bipartite exactly when no odd cycle | 5 | [[2026-07-24 Preliminaries]] |
| Bipartition unique when connected | 5 | [[2026-07-29 Matchings 2 — Berge and König]] |
| Birkhoff and von Neumann | 7 | [[Lec 03 — More on Hall's Theorem and Applications]] |
| Components partition the vertex set | 1 | [[Assignment 1]] Q11 |
| Defect Hall | 7 | [[Lec 03 — More on Hall's Theorem and Applications]] |
| Degeneracy matches greedy deletion | 3 | Bridge 3.2 |
| Density k gives a subgraph with δ ≥ k | 3 | [[2026-07-24 Preliminaries]] |
| Diameter k and min degree d give about kd/3 vertices | 3 | [[Assignment 1]] Q10 |
| Distance layers | 1 | [[Assignment 1]] Q5 |
| Euler's formula n − m + f = 2 | 9 | Bridge 9.1 |
| Euler's theorem, both lemmas | 6 | [[2026-07-27 Euler Circuits]] |
| Euler's theorem by maximal trail | 6 | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] |
| Forest exchange property | 4 | [[Assignment 1]] Q22 |
| Gallai, α + β = n | 7 | [[Lec 01 — Vertex Cover and Independent Set]] |
| Gallai, α′ + β′ = n | 7 | [[Lec 01 — Vertex Cover and Independent Set]] |
| Girth at most 2·diam + 1 | 1 | [[Assignment 1]] Q4 |
| Girth 5 gives δ ≤ √(n−1) | 3 | [[Assignment 1]] Q8 |
| Hall's marriage theorem | 7 | [[Lec 02 — König's Theorem and Hall's Theorem]] |
| Handshake lemma | 3 | [[2026-07-24 Preliminaries]] |
| Handshake parity corollary | 3 | Bridge 3.1 |
| Helly property in one dimension | 2 | [[Tutorial 1]] Q6 |
| Hypercube invariants | 5 | [[Tutorial 1]] Q1 · [[Assignment 1]] Q2 |
| Induced path on three vertices exists | 1 | [[Tutorial 1]] Q3 |
| k regular bipartite gives a perfect matching | 7 | [[Lec 03 — More on Hall's Theorem and Applications]] |
| k regular of girth 5 needs k²+1 vertices | 3 | [[Tutorial 1]] Q2 |
| König's theorem | 7 | [[Lec 02 — König's Theorem and Hall's Theorem]] · [[2026-07-29 Matchings 2 — Berge and König]] |
| Königsberg is impossible | 6 | [[2026-07-27 Euler Circuits]] |
| Latin rectangle extension | 7 | [[Lec 03 — More on Hall's Theorem and Applications]] |
| Leaf edge lies in some maximum matching | 7 | [[2026-07-29 Matchings 2 — Berge and König]] |
| Lemma A, δ ≥ k gives a long path | 2 | [[2026-07-24 Preliminaries]] |
| Lemma B, δ ≥ 2 gives a cycle | 2 | [[2026-07-24 Preliminaries]] |
| Lemma C, δ ≥ k gives a cycle of length k+1 | 2 | [[2026-07-24 Preliminaries]] |
| Long path theorem | 2 | [[2026-07-24 Long Path Theorem]] |
| m > C(n−1,2) gives connectedness | 3 | [[2026-07-24 Preliminaries]] |
| Maximal versus longest | 2 | [[2026-07-24 Preliminaries]] |
| Min degree cannot force k connectivity | 8 | [[Assignment 1]] Q14 |
| Min-max duality family | 7 | Bridge 7.1 |
| MIS in a tree by dynamic programming | 4 | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] |
| MIS in a tree by greedy on leaves | 4 | [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] |
| Moon and Moser, at most 3 to the n over 3 maximal independent sets | 4 | [[2026-07-29 Matchings 2 — Berge and König]] |
| Moore bound | 3 | [[Assignment 1]] Q7 |
| Odd cycle is not bipartite | 5 | [[2026-07-24 Preliminaries]] |
| Path or cycle of length at least min{2δ, n} | 2 | [[Assignment 1]] Q9 |
| Petersen, bridgeless cubic gives a 1 factor | 7 | [[2026-08-19 Tutte's 1-Factor Theorem]] |
| Q₄ is not planar | 9 | [[Tutorial 1]] Q1 |
| rad ≤ diam ≤ 2·rad | 1 | [[Assignment 1]] Q6 |
| SDR criterion | 7 | [[Lec 03 — More on Hall's Theorem and Applications]] |
| Shortest paths are induced | 1 | [[Tutorial 1]] Q5 |
| Subgraph, induced, spanning | 0 | Bridge 0.1 |
| The sandwich α′ ≤ β ≤ 2α′, both ends tight | 7 | [[2026-07-29 Matchings 2 — Berge and König]] |
| The union of two matchings has degree at most 2 | 7 | [[2026-07-29 Matchings 2 — Berge and König]] |
| Tree characterisations, Theorem 1.5.1 | 4 | [[Assignment 1]] Q19 |
| Tree has at least Δ(T) leaves | 4 | [[Assignment 1]] Q20 |
| Tree with no degree 2 vertex has L ≥ I + 2 | 4 | [[Assignment 1]] Q21 |
| Tree has n−1 edges and unique paths | 4 | [[2026-07-24 Preliminaries]] |
| Tree order is a partial order | 4 | [[Assignment 1]] Q23 |
| Tutte's 1-factor theorem | 7 | [[2026-08-19 Tutte's 1-Factor Theorem]] |
| Two longest paths meet | 2 | [[Tutorial 1]] Q4 |
| Vertex in every maximum matching, bipartite | 7 | [[2026-08-10 Matchings in Bipartite Graphs]] |
| Vertices in every maximum matching number at least β | 7 | [[2026-08-10 Matchings in Bipartite Graphs]] |
| Walk contains a path | 1 | Bridge 1.1 |
| Adding a vertex joined to k others keeps k-connectedness | 8 | [[2026-08-31 Blocks, Ear Decomposition, and k-Connectivity]] |
| Block, and why a bridge is one | 8 | [[2026-08-31 Blocks, Ear Decomposition, and k-Connectivity]] |
| Block graph of a connected graph is a tree | 8 | [[2026-08-31 Blocks, Ear Decomposition, and k-Connectivity]] |
| Dirac, δ ≥ n/2 gives a Hamiltonian cycle | 8 | [[2026-08-31 Connectivity 1 — Minimum Degree and Whitney's Theorem]] |
| Ear decomposition characterises 2-connectedness | 8 | [[2026-08-31 Blocks, Ear Decomposition, and k-Connectivity]] |
| Four consequences of 2-connectedness | 8 | [[2026-08-31 Blocks, Ear Decomposition, and k-Connectivity]] |
| Minimum degree (n−1)/2 forces connectedness | 8 | [[2026-08-31 Connectivity 1 — Minimum Degree and Whitney's Theorem]] |
| Subdividing an edge preserves 2-connectedness | 8 | [[2026-08-31 Blocks, Ear Decomposition, and k-Connectivity]] |
| Union of two l-connected graphs, and its hypothesis | 8 | [[2026-08-31 Blocks, Ear Decomposition, and k-Connectivity]] |
| Whitney, 2-connected means two disjoint paths | 8 | [[2026-08-31 Connectivity 1 — Minimum Degree and Whitney's Theorem]] |
| α ≤ β and α′ ≤ ⌊n/2⌋ | 7 | [[Lec 01 — Vertex Cover and Independent Set]] |
| 2k regular gives a 2 factor | 7 | [[2026-08-10 König by Induction, Hall, and Factors]] |
| δ ≥ 3 gives an even cycle | 2 | [[2026-07-24 Preliminaries]] |
| κ ≤ λ ≤ δ, and values for standard families | 8 | [[Assignment 1]] Q13 |

# If I only remember five things

1. The extremal method, Level 2. Take something maximal and ask what un-extendability forces. Nine results, one idea.
2. Count two ways, Level 3. Handshake and everything descended from it.
3. Maximal is not the same as maximum, and maximal is nearly always enough and far cheaper.
4. Parity decides more than it has any right to: bipartiteness, even cycles, Euler circuits, odd degree counts, odd components.
5. Min-max duality, Bridge 7.1. König, Hall, Menger, max-flow min-cut and Dilworth are one theorem in five costumes.
