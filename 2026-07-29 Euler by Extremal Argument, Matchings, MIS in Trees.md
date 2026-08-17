---
tags: [academics, graph-theory, lecture]
date: 2026-07-29
seq: 4
class: 3
---

# 4 · 2026-07-29 — Euler by Extremal Argument, Matchings, MIS in Trees

**◀ Previous:** [[2026-07-27 Euler Circuits]]  ·  **Hub:** [[Graph Theory]]  ·  **Next ▶** [[2026-07-29 Matchings 2 — Berge and König]]

**Covered:** a second proof of Euler's Lemma 2 using a maximal trail, the definition of matchings with bounds for standard families, and finding a maximum independent set in a tree.

---

## 0. Symbols used today

| Symbol | Meaning |
|---|---|
| **Q** | a trail (walk with no repeated **edges**) |
| **E(Q), V(Q)** | the edge set / vertex set of Q |
| **maximal trail** | a trail that **cannot be extended** at either end |
| **ν(G)** | maximum matching size |
| **MIS** | maximum independent set |
| **leaf** | a vertex of degree 1 |
| **n** | number of vertices |

---

# Part A — Euler's Lemma 2 again, by extremal argument

In [[2026-07-27 Euler Circuits]] I proved Lemma 2 by **induction on the number of edges** (pull out a cycle, recurse, splice). Today's class gave a **different and shorter proof**: grab a *maximal* trail and show it must already be everything.

> **Lemma 2.** If G has at most one non-trivial component and every vertex has even degree, then G has an **Euler circuit**.

**The whole idea:** take a trail you cannot extend. Show (a) it must be closed, and (b) it must already contain every edge. Then it *is* an Euler circuit.

---

## ⚠️ First, clear up two confusions from my notes

**"Is every cycle maximal?"** — **No.** In my notes I wrote `abefa = befab`, which just says a closed trail can be written starting from any of its vertices. That's not the issue. The real point:

> **A cycle can fail to be maximal.** In the graph below, `a–b–e–f–a` is a closed trail, but the edge `bc` at vertex b is unused, so the trail extends.

```
   a ——— b ——— c
   |     |
   f ——— e ——— d
```

Here `abefa` is a cycle but **not a maximal trail** — from b you can continue along bc. Maximal means *no unused edge at either endpoint*, which is stronger than *closed*.

**"A trail does not have to be closed"** — correct. `a–b–c` is a perfectly good trail and it's open. What we're about to prove is that a **maximal** trail *cannot* be open, under our even-degree hypothesis.

---

## Claim 1 — a maximal trail is closed

> **Claim 1.** If every vertex of G has even degree, then any **maximal** trail Q is **closed** (starts and ends at the same vertex).

**Proof of Claim 1.** Suppose Q is open, running from u to a different endpoint v.

Count the edges of Q at the vertex **v**. Every time the trail *passes through* v it consumes **2** edges (one in, one out). But the trail *ends* at v, so the final arrival consumes **1** more. Total edges of Q at v:

$$\underbrace{2 \times (\text{number of passes through } v)}_{\text{even}} \;+\; \underbrace{1}_{\text{the final arrival}} \;=\; \textbf{odd}.$$

But **deg(v) is even** by hypothesis. An even number cannot equal an odd number, so **not all** of v's edges are used by Q — at least one is left over.

*(This is the "odd vertex" remark in my notes: an open trail makes its endpoint behave like an odd-degree vertex.)*

Take an unused edge at v and append it. That's a longer trail, so **Q was not maximal** ✗

Contradiction. Hence Q is closed ✓ ∎

> Since Q is a **closed trail**, it is a **circuit** — matching the definition from [[2026-07-27 Euler Circuits]] §0.

---

## Claim 2 — a maximal trail uses every edge

> **Claim 2.** Under the hypotheses of Lemma 2, a maximal trail Q satisfies **E(Q) = E(G)**.

**Proof of Claim 2.** Suppose not, so some edge of G is missing from Q. We find a contradiction by building a longer trail.

**Step 2.1 — find a missing edge that touches Q.**

There are two cases, and both hand us a missing edge with an endpoint **on** Q.

- **Case (i): some missing edge (x, y) already touches Q**, i.e. x ∈ V(Q) or y ∈ V(Q). Take **e := (x, y)** and let **z** be whichever endpoint lies on Q.
- **Case (ii): no missing edge touches Q.** Take any missing edge (x, y). Since G's edges all live in one non-trivial component, there's a path from x to Q. Take a **shortest** such path and let **e** be its **last** edge, say e = (w, z) with **z ∈ V(Q)**.

  Why is e itself missing from Q? Because we chose a *shortest* path to Q: every vertex before z is off Q, so e is not one of Q's edges ✓

*(This case split is exactly the side-note in my page: "if x ∈ V(Q) let z = x, else if y ∈ V(Q) let z = y".)*

**Step 2.2 — build the longer trail.**

By **Claim 1**, Q is a **closed** trail, so it can be started at **any** of its vertices — in particular at **z**.

```
        ┌──────── traverse all of Q ────────┐
        │                                    │
        z ────────────────────────────────► z ────e────► (other end of e)
                (closed, so we return)         unused edge
```

Walk the whole of Q starting and ending at z, then step along **e**. Since e ∉ E(Q), no edge repeats — this is a genuine trail, and it has **one more edge** than Q.

So Q was not maximal ✗ **Contradiction.**

Hence our assumption was wrong and **E(Q) = E(G)** ✓ ∎

---

## Combining the claims

- **Claim 1** ⇒ Q is a closed trail, i.e. a **circuit**.
- **Claim 2** ⇒ Q contains **every edge** of G.

A circuit containing every edge is exactly an **Euler circuit**. So G has one ✓ ∎

> **Why this proof is nicer than the induction.** The induction version had a genuinely fiddly step — after deleting a cycle the graph can shatter, so you must recurse on each piece and splice them back ([[2026-07-27 Euler Circuits]], Lemma 2 Step 4). The maximal-trail argument never splits the graph at all. It's the same **extremal method** used for the long-path theorem: *take an object you can't extend, and let un-extendability do the work.*

---

# Part B — Matchings

> A **matching** is a set of edges in which **no two edges share a vertex**.

*(Equivalently: no two edges of the set are incident on a common vertex.)*

**From the example in class** — the graph on a, b, c, d, e, f, g:

| Set | Verdict |
|---|---|
| {ab, cd, ef} | ✅ a matching — all six endpoints distinct |
| {ab, ag} | ❌ **a is common** to both edges |
| {gf, ad, bc} | ✅ a matching |

---

## Claim 3 — the universal ceiling ν(G) ≤ ⌊n/2⌋

**Proof of Claim 3.** A matching with ν edges uses **2ν distinct vertices** — distinct precisely because no two edges share one. Those vertices all live in G, so

$$2\nu \le n \quad\Longrightarrow\quad \nu \le \frac{n}{2}.$$

And ν is a whole number, so **ν ≤ ⌊n/2⌋** ✓ ∎

> ⚠️ **Notation fix from my notes:** I wrote `|matchings(G)| ≤ n/2`. That reads as "the *number of* matchings", which isn't what's meant. The correct statement is about the **size of a maximum matching**, written **ν(G)**.

---

## Values for the standard families

| Graph | ν | Why |
|---|---|---|
| **Path Pₙ** (n vertices) | ⌊n/2⌋ | take every other edge |
| **Cycle Cₙ** | ⌊n/2⌋ | same, walking round |
| **Star K₁,ₘ** | **1** | every edge hits the centre |
| **Complete Kₙ** | ⌊n/2⌋ | pair the vertices off |
| **Tree** | anywhere from **1 to ⌊n/2⌋** | a star gives 1; a perfect-matchable tree gives n/2 |

**Star — the interesting case.** Every edge of K₁,ₘ contains the centre c. So any two edges share c, and a matching can hold **at most one** edge. Hence ν = 1 ✓ This is the extreme where the ceiling ⌊n/2⌋ is as loose as possible.

**Path P₄ = a–b–c–d.** Take {ab, cd}: ν = 2 = ⌊4/2⌋ ✓
**Path P₅ = a–b–c–d–e.** Take {ab, cd}: ν = 2 = ⌊5/2⌋ ✓ (e is left over — with 5 vertices somebody must be.)

> **Open question in my notes:** *"maximum matching in a tree — number of levels + 1/2?"* That guess doesn't hold: a star has many vertices but only **1** level below the root and ν = 1, while a long path has ν ≈ n/2. The level count doesn't determine ν. **There's no formula in terms of depth** — you need an actual algorithm (greedy on leaves works, same idea as Part C).

---

# Part C — Maximum Independent Set in a tree

> **Problem.** Given a tree or forest, find a **maximum independent set** — a largest subset of vertices with **no edge between any two of them**.

*(Recall from [[Lec 01 — Vertex Cover and Independent Set]]: this is NP-hard in general. On trees it turns out to be easy.)*

---

## Strategy 1 — split by level. **This fails.**

Root the tree and set

- **O** = all vertices at **odd** levels
- **E** = all vertices at **even** levels

Both are independent (every edge joins consecutive levels, so it never has both ends in O or both in E). The proposal is **MIS = max{|O|, |E|}**.

### Counterexample

Root **r** with four children a, b, c, d; and a additionally has two children e, f.

```
            r                level 0   →  E
         ╱ ╱ ╲ ╲
        a  b  c  d           level 1   →  O
       ╱ ╲
      e   f                  level 2   →  E
```

- **E** = {r, e, f} → size **3**
- **O** = {a, b, c, d} → size **4**
- so the method returns **4**

But **{b, c, d, e, f}** is independent — b, c, d are leaves hanging off r, and e, f hang off a; none of the five is adjacent to another. That's size **5 > 4** ✗

**The method fails.** Splitting by level is too rigid: it forces you to take *all* of one side, when the best answer mixes levels.

---

## Strategy 2 — greedy on leaves. **This works.**

> 1. Put **all leaves** into the solution.
> 2. **Delete** the leaves and their parents, then **recurse** on what remains.

The whole correctness rests on one exchange argument.

### Claim 4 — some maximum independent set contains any given leaf

> **Claim 4.** Let u be a leaf of a tree T. Then **there exists** a maximum independent set of T containing u.

**Proof of Claim 4.** Let S be *any* maximum independent set, and let **p** be the unique neighbour (parent) of u.

**Case (i): u ∈ S.** Nothing to do ✓

**Case (ii): u ∉ S.** First, note **p must be in S**:

> if p ∉ S, then S ∪ {u} would still be independent — u's *only* neighbour is p, and p ∉ S — and it is strictly bigger than S, contradicting that S is **maximum** ✗

So p ∈ S. Now **swap**:

$$S' := \big(S \setminus \{p\}\big) \cup \{u\}.$$

- **S′ is independent.** The only vertex adjacent to u is p, and we just removed it. Nothing else changed ✓
- **|S′| = |S|.** We removed one vertex and added one ✓ so S′ is still **maximum**.
- **u ∈ S′** ✓

Either way, a maximum independent set containing u exists ∎

### Why Claim 4 makes the greedy correct

Claim 4 says **taking a leaf never costs you anything** — there's always an optimal solution that agrees with that choice. Having committed to leaf u:

- **p cannot** also be chosen (it's adjacent to u), so deleting p loses nothing.
- Deleting u and p leaves a smaller forest, and the same argument applies again.

So the greedy is safe at every step, and it terminates because the forest shrinks each round ✓

**Run it on the counterexample above.**

- **Round 1:** leaves are b, c, d, e, f. Take all five. Their parents are r (for b, c, d) and a (for e, f) — delete r and a too.
- Nothing remains.
- **Answer: {b, c, d, e, f}, size 5** ✓ — the correct MIS, which Strategy 1 missed.

> **The transferable idea — an exchange argument.** To prove a greedy choice is safe, take *any* optimal solution and show you can **modify it** into one that agrees with your choice, **without making it worse**. Here the modification was a one-for-one swap: drop the parent, add the leaf.

---

## Takeaways

1. **Maximal trail ⇒ Euler circuit**, in two claims: it must be *closed* (Claim 1), and it must be *everything* (Claim 2).
2. **An open trail makes its endpoint look odd-degree** — that parity clash is the whole content of Claim 1.
3. A **closed** trail can be restarted at any of its vertices. That's exactly what lets Claim 2 splice on an extra edge.
4. **Maximal ≠ cycle.** A cycle can still have unused edges hanging off it.
5. **ν(G) ≤ ⌊n/2⌋** always, because a matching's edges are vertex-disjoint. Stars are the extreme case, with ν = 1 however large they get.
6. **Level-splitting fails** for MIS on trees — the optimum mixes levels.
7. **Greedy on leaves works**, justified by an **exchange argument**: any optimal solution can be swapped into one containing the leaf.

---

## Doubts / to revisit

- [ ] My notes asked whether maximum matching in a tree is "number of levels + 1/2" — **no**, disproved by the star above. Worth asking what the intended formula was.
- [ ] Notation: I wrote `|matchings(G)| ≤ n/2`; should be **ν(G) ≤ ⌊n/2⌋** (size of a maximum matching, not the number of matchings).
- [ ] The greedy-on-leaves argument gives an O(n) algorithm — worth writing out as pseudocode if it's examinable.
