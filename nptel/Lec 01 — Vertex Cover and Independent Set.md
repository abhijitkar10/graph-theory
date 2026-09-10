---
tags: [academics, graph-theory, nptel, lecture]
lecture: 1
unit: Covering Problems
source: NPTEL Graph Theory (Dr. L. Sunil Chandran, IISc), Lecture 01
---

# Lec 01 — Introduction, vertex cover and independent set

Previous: none, this is the first lecture · Index: [[NPTEL Index]] · Next: [[Lec 02 — König's Theorem and Hall's Theorem]]

Covered here: the four covering and packing parameters, how two of them are complements, both Gallai identities, the inequality α′ ≤ β, and why these problems are computationally hard.

These are my own written up versions of the mathematics, with statements, proofs and examples reconstructed from scratch rather than transcribed from the video. Where a proof can go several ways I give the cleanest standard route and mention the alternatives.

## How much this matters

Overall this note is useful. Everything in it also appears in the class notes, so treat it as a second pass rather than new material.

Know cold: [[Lec 01 — Vertex Cover and Independent Set#Independent sets and vertex covers are complements|the complement theorem]] and the first Gallai identity that follows from it. Two lines each, and they carry the whole note.

Know the argument: [[Lec 01 — Vertex Cover and Independent Set#The second Gallai identity|the second Gallai identity]], especially the star decomposition of a minimum edge cover, and [[Lec 01 — Vertex Cover and Independent Set#The matching number never exceeds the cover number|why α′ ≤ β]].

Read once: [[Lec 01 — Vertex Cover and Independent Set#Why these problems are hard|the complexity section]]. Useful context, unlikely to be examined.

## Notation

The course uses West's letters, and I use them here too. α(G) is the independence number, the size of the largest independent set. β(G) is the vertex cover number, the size of the smallest vertex cover. α′(G) is the matching number, the size of the largest matching. β′(G) is the edge cover number, the size of the smallest edge cover. Also ω(G) is the clique number, the size of the largest clique, and the complement of G has the same vertices with edges exactly where G has none. As usual n is the number of vertices.

The pattern to hold on to is that α means packing and you maximise, β means covering and you minimise, unprimed refers to vertices and primed to edges. The NPTEL lectures write ν for α′, τ for β and ρ for β′, which are the same four objects.

## The four definitions

A set S of vertices is independent when no edge has both of its endpoints in S. Think of it as a set of mutually non adjacent vertices, no two of which see each other.

A set K of vertices is a vertex cover when every edge has at least one endpoint in K. Think of it as putting guards on vertices so that every edge is watched from at least one end.

```
   a ——— b        {a, c} is independent, since there is no edge ac
   |     |        {a, b} is not, since ab is an edge
   d ——— c        K = {a, c} is a vertex cover: ab and da are watched
                  from a, and bc and cd from c
```

A set M of edges is a matching when no two of its edges share a vertex. Think of pairing people up so that nobody is in two pairs.

A set F of edges is an edge cover when every vertex is an endpoint of some edge in F. Every vertex must be touched by at least one chosen edge.

An edge cover exists only when G has no isolated vertex, since a vertex with no edges can never be covered. Assume that throughout whenever β′ appears.

The symmetry is worth noticing, because these are the same idea with vertices and edges swapped.

| | packing, maximise, disjointness | covering, minimise, hit everything |
|---|---|---|
| vertices | independent set α | vertex cover β |
| edges | matching α′ | edge cover β′ |

## Independent sets and vertex covers are complements

Theorem. S is an independent set exactly when the complement of S is a vertex cover.

Given: a set S of vertices.
To show: the two conditions are the same condition.

Chase the definitions, because both sides say the same thing about edges. S is independent means no edge has both ends in S, which is the same as saying every edge has at least one end outside S, which is the same as saying every edge has at least one end in the complement of S. That last phrase is precisely the definition of the complement being a vertex cover.

### The first Gallai identity

Corollary. α(G) + β(G) = n.

Take a maximum independent set S, of size α. Its complement is a vertex cover of size n − α, so β is at most n − α, giving α + β ≤ n.

Now take a minimum vertex cover K, of size β. Its complement is independent of size n − β, so α is at least n − β, giving α + β ≥ n.

Both together give equality.

Check it on the four cycle a–b–c–d–a. Here α = 2, taking {a,c}, and β = 2, taking the same set, and n = 4. Check it on K₅. Here α = 1, since any two vertices are adjacent, and β = 4, and n = 5.

The point is that the two problems are the same problem wearing different clothes. Solve one and you have solved the other, and in particular if one is computationally hard then so is the other.

### A third disguise, cliques

A set S is independent in G exactly when S is a clique in the complement of G. Independent in G means no edges inside S, and in the complement every non edge of G becomes an edge, so S becomes pairwise adjacent. Hence α(G) equals the clique number of the complement.

So independent set, vertex cover and clique are three views of one problem.

## The matching number never exceeds the cover number

Theorem. In every graph, α′(G) ≤ β(G).

Given: a maximum matching M, of size α′, and any vertex cover K.
To show: K has at least α′ vertices.

K must cover every edge, in particular every edge of M, so for each of the α′ edges of M it contains at least one of the two endpoints. The edges of M are pairwise disjoint, which is what makes M a matching, so those chosen endpoints are α′ distinct vertices, all sitting inside K. Hence K has at least α′ vertices.

That holds for every vertex cover, so it holds for the smallest one, which gives β ≥ α′.

```
 M = three disjoint edges          any cover needs at least one vertex
 ●━━●    ●━━●    ●━━●              per edge, and the edges share nothing,
                                   so at least 3 vertices are needed
```

When is it equality and when is it strict? The triangle has α′ = 1, since any two of its edges share a vertex, and β = 2, since one vertex misses the opposite edge, so the inequality is strict there. Every bipartite graph gives equality, which is König's theorem, the subject of [[Lec 02 — König's Theorem and Hall's Theorem]].

The odd cycle is the obstruction. The triangle is the smallest example where α′ < β, and bipartite graphs are exactly the graphs with no odd cycle, as shown in [[2026-07-24 Preliminaries]]. That is not a coincidence, and it is the whole reason König's theorem needs bipartiteness.

## The second Gallai identity

Theorem. If G has no isolated vertices then α′(G) + β′(G) = n.

This is the edge side twin of the first identity. The proof is prettier, because the two directions are built by different constructions.

### First direction, β′ ≤ n − α′

Take a maximum matching M, with α′ edges. It covers exactly 2α′ vertices, leaving n − 2α′ untouched. Since there are no isolated vertices, each untouched vertex has some edge, so pick one such edge per untouched vertex and add it in.

```
 matched pairs:  ●━━●  ●━━●          2α′ vertices covered by α′ edges
 leftovers:      ●  ●  ●             each grabs one edge of its own
                 └┐ └┐ └┐
```

The result covers every vertex, so it is an edge cover, and it uses α′ + (n − 2α′) = n − α′ edges. Hence β′ ≤ n − α′.

### Second direction, α′ ≥ n − β′

Take a minimum edge cover F, with β′ edges, and look at F as a subgraph.

Claim: every component of F is a star, meaning one centre joined to some leaves.

Suppose some component contained a path on four vertices u, v, w, x. Then the middle edge vw is redundant, since u and v are still covered by uv, and w and x by wx. Dropping it would give a smaller edge cover, contradicting minimality. Similarly no component contains a cycle, since dropping any cycle edge leaves its endpoints covered by the neighbouring cycle edges. So each component is a tree containing no path on four vertices, which is exactly a star.

Now count. Let the components be stars with k₁, …, k_c edges. A star with kᵢ edges has kᵢ + 1 vertices, and every vertex of G lies in exactly one component since F covers everything. So the sizes kᵢ + 1 add to n while the kᵢ add to β′, which gives c = n − β′.

Pick one edge from each star. Different stars are vertex disjoint, so those c edges form a matching, giving α′ ≥ c = n − β′.

### Combining

The first direction gives α′ + β′ ≤ n and the second gives α′ + β′ ≥ n, so the two are equal.

Check it on the path a–b–c, where n = 3. Here α′ = 1, since ab and bc share b, and β′ = 2, since both edges are needed to touch a and c, and 1 + 2 = 3. On the four cycle, α′ = 2 and β′ = 2, adding to 4. On K₄, α′ = 2 by a perfect matching and β′ = 2, again adding to 4.

Both identities in one line: α + β = n pairs a maximum independent set with a minimum vertex cover, and α′ + β′ = n pairs a maximum matching with a minimum edge cover. In each case, solving the maximisation problem hands you the minimisation problem for free.

## Why these problems are hard

Vertex cover is one of Karp's original 21 NP-complete problems, from 1972. By the complement identity above, so are independent set and clique, and an efficient algorithm for any one of them would solve all three.

| Problem | General graphs | Bipartite graphs |
|---|---|---|
| maximum matching α′ | polynomial, by Edmonds' blossom algorithm | polynomial, by Hopcroft and Karp |
| minimum vertex cover β | NP-hard | polynomial, via König since β = α′ |
| maximum independent set α | NP-hard | polynomial, via α = n − β |

So bipartiteness collapses a hard problem into an easy one, entirely because König's theorem forces α′ = β there. That single equality is why the next lecture matters so much.

## Summary of relationships

The three facts are α + β = n, and α′ + β′ = n when there are no isolated vertices, and α′ ≤ β. Combining the first and third gives α′ ≤ β = n − α.

On the four cycle, with n = 4, all four parameters equal 2, since it is bipartite. On the triangle, with n = 3, we have α = 1, β = 2, α′ = 1 and β′ = 2. Both identities check out, and α′ = 1 is strictly below β = 2, which is right because the triangle is not bipartite.

## What to remember

Independent set and vertex cover are complements, one set with two names, and everything else in this lecture follows from that. Cliques are the same problem again, viewed in the complement graph. The inequality α′ ≤ β holds always, because a matching's edges are disjoint and each demands its own cover vertex, and odd cycles are what break the equality, with the triangle as the minimal witness. Both Gallai identities say that the maximum packing and the minimum covering add to n, and both proofs are constructions rather than counting arguments: extend a maximum matching to an edge cover, and pick one edge per star. Minimum edge covers decompose into stars, because any longer path would contain a droppable middle edge. And bipartiteness turns NP-hard into polynomial, via König.

## Still unclear

- The lecture's exact route for α′ + β′ = n. I used the maximum matching extension proof, which is standard. Some courses derive it from König instead.
- Edmonds' blossom algorithm is mentioned here but not proved. It comes later in the matchings unit.
