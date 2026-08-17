---
tags: [academics, graph-theory, lecture]
date: 2026-07-29
seq: 5
class: 3
---

# 5 · 2026-07-29 — Matchings 2: Berge and König

**◀ Previous:** [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]]  ·  **Hub:** [[Graph Theory]]  ·  **Next ▶** [[Tutorial 1]]

**Covered:** matching bounds for standard families, matchings in trees (the leaf claim), alternating and augmenting paths, **Berge's theorem** in both directions, vertex covers, the sandwich |MM| ≤ |MVC| ≤ 2|MM|, and **König's theorem** with its explicit A₀/B₁/A₁/B₂/A₂ construction.

> Same afternoon as the morning class ([[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]]), going much deeper into matchings.

---

## 0. Symbols used today

| Symbol | Meaning |
|---|---|
| **M** | a matching — a set of edges, no two sharing a vertex |
| **\|MM(G)\|** | size of a **maximum matching** *(the standard symbol is ν(G))* |
| **\|MVC(G)\|** | size of a **minimum vertex cover** *(standard: τ(G))* |
| **\|MIS(G)\|** | size of a **maximum independent set** *(standard: α(G))* |
| **V(M)** | the set of vertices **covered** (matched) by M |
| **M-alternating path** | a path whose edges alternate in M / not in M |
| **M-augmenting path** | an M-alternating path whose **two endpoints are both unmatched** |
| **M △ P** | symmetric difference — written in class as **M∖P + P∖M** |

> **Notation bridge.** My class writes |MM|, |MVC|, |MIS|; textbooks (and my NPTEL notes) write **ν, τ, α**. Same objects. → [[Lec 01 — Vertex Cover and Independent Set]]

---

## 1. Matchings — definition and first bounds

> A **matching** is a set of edges where **no two edges of the set are incident on a common vertex**.

**From the class example** on a, b, c, d, e, f, g:

| Set | Verdict |
|---|---|
| {ab, cd, ef} | ✅ matching |
| {ab, ag} | ❌ **a is common** |
| {gf, ad, bc} | ✅ matching |

### The universal ceiling

$$|MM(G)| \;\le\; \frac{n}{2}$$

because a matching of size ν uses 2ν **distinct** vertices. → proved in [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] Claim 3.

### Values for the standard families

| Graph | \|MM\| | \|MIS\| | \|MVC\| = n − \|MIS\| | MM vs MVC |
|---|---|---|---|---|
| **Path Pₙ** | ⌊n/2⌋ | ⌈n/2⌉ | ⌊n/2⌋ | **=** |
| **Cycle Cₙ** | ⌊n/2⌋ | ⌊n/2⌋ | ⌈n/2⌉ | **=** if n even, **<** if n odd |
| **Star Sₙ** | 1 | n−1 | 1 | **=** |
| **Complete Kₙ** | ⌊n/2⌋ | 1 | n−1 | **<** (for n ≥ 3) |
| **Tree T** | k | n−k | k | **=** |

> ★ **The third column is Gallai's identity in disguise:** α + τ = n, so **|MVC| = n − |MIS|**. That's why the table computes n − |MIS| rather than τ directly. → [[Lec 01 — Vertex Cover and Independent Set]] §2

> **Read the last column.** Equality holds for paths, stars, trees and *even* cycles — all **bipartite**. It fails for Kₙ and *odd* cycles — the non-bipartite ones. That pattern is exactly König's theorem, coming in §6.

---

## 2. Matchings in trees and forests

### ⚠️ Correction — Moon & Moser (1965)

My page says *"No. of maximum ind. set = 3^(n/3)"* with the picture of disjoint triangles. Two fixes:

- It counts **maximal** independent sets (can't be extended), **not maximum** ones.
- It's an **upper bound on how many there are**, not the size of one.

> **Moon–Moser (1965).** A graph on n vertices has at most **3^(n/3)** maximal independent sets, and this is attained by **n/3 disjoint triangles** (pick one vertex from each triangle — 3 choices, independently).

```
   △   △   △   ...   △        n/3 triangles
   T₁  T₂  T₃         T_{n/3}    → 3 × 3 × … × 3 = 3^(n/3) maximal ind. sets
```

### ★ Claim — a leaf's edge lies in some maximum matching

> **Claim.** Let **u** be a leaf and **v** its unique neighbour. Then the edge **uv** belongs to *some* maximum matching.

*(This is the matching twin of the MIS leaf claim from the morning class — same exchange-argument shape.)*

**Structure:** two cases on whether v is matched.

Let M be any maximum matching.

**Case 1 — no edge of M touches u.**

Then u ∉ V(M). Sub-split on v:

- If **v ∉ V(M)** too, then **M + uv** is still a matching (neither endpoint was used) and is **strictly bigger** ✗ contradicting maximality. So this can't happen.
- Hence **v ∈ V(M)** — v is matched, say by the edge **vx ∈ M**.

Now **swap**: set

$$N := M - vx + uv .$$

- **N is a matching:** we freed v by dropping vx, and u was unmatched, so uv clashes with nothing ✓
- **|N| = |M|** — one edge out, one in ✓ so N is still **maximum** ✓
- **uv ∈ N** ✓

**Case 2 — some edge of M touches u.**

u is a leaf, so its only edge is uv. Hence **uv ∈ M** already, and M itself is the maximum matching we wanted ✓

**Combining:** in both cases a maximum matching containing uv exists ∎

> **The transferable idea — exchange argument again.** Take *any* optimum, and show you can **modify** it to agree with your greedy choice **without shrinking it**. Same move as the MIS leaf claim. This is what makes "grab a leaf edge and recurse" a correct algorithm on trees.

---

## 3. Alternating and augmenting paths

> An **M-alternating path** is a path whose edges alternate between **being in M** and **not being in M**.

> An **M-augmenting path** is an M-alternating path that **starts and ends at unmatched vertices**.

```
 unmatched                                   unmatched
    ●━━━━━━━●═══════●━━━━━━━●═══════●━━━━━━━●
      ∉M      ∈M      ∉M      ∈M      ∉M
```

An augmenting path has an **odd** number of edges: it begins and ends with non-M edges, so it carries **one more** non-M edge than M edges.

> **Also noted in class:** if there is an edge uv with **u ∉ V(M) and v ∉ V(M)**, then M is not maximum — in fact **not even maximal**, since you could simply add uv. That single edge is the shortest possible augmenting path.

---

## 4. ★ Berge's Theorem

> **Theorem (Berge / Petersen).** A matching M is **not maximum** ⟺ there exists an **M-augmenting path** in G.

Two lemmas, one per direction.

---

### Lemma 1 (⇐) — an augmenting path means M isn't maximum

> **Lemma 1.** If there exists an M-augmenting path P in G, then M is not a maximum matching.

**Proof.** Form

$$M' \;:=\; (M \setminus P) \;+\; (P \setminus M)$$

— throw out the M-edges lying on P, and take in the non-M edges of P instead. *(This is the symmetric difference M △ P.)*

**Claim 1.1 — M′ is a matching.**
Along P the swap gives each interior vertex a new partner in place of its old one, so no interior vertex ends up in two edges. The **two endpoints were unmatched**, so the new edges there clash with nothing. Off P, nothing changed ✓

**Claim 1.2 — |M′| = |M| + 1.**
P is augmenting, so it holds **one more** non-M edge than M edges. We removed the M-edges of P and added the non-M edges, so the count goes up by exactly 1 ✓

**Combining:** M′ is a **bigger** matching, so M was not maximum ∎

```
 before:  ●━━━●═══●━━━●        1 M-edge
 after:   ●═══●━━━●═══●        2 M-edges  ← gained one
```

---

### Lemma 2 (⇒) — if M isn't maximum, an augmenting path exists

> **Lemma 2.** If M is not a maximum matching, then G contains an M-augmenting path.

**Proof.** Since M is not maximum, take a matching **N** with **|N| > |M|**. Build the graph

$$H \;:=\; M \cup N, \qquad V(H) = V(G), \qquad E(H) = E(M) \cup E(N).$$

**Claim 2.1 — Δ(H) ≤ 2.**
At any vertex there is **at most one** edge from M and **at most one** from N, since both are matchings. So degree ≤ 2 in H ✓

*(My page notes |E(M)| ≤ ⌊n/2⌋ and |E(N)| ≤ ⌊n/2⌋, so |E(H)| < n — consistent with max degree 2.)*

**Claim 2.2 — H is a disjoint union of paths and cycles, and every cycle is even.**
Max degree ≤ 2 forces every component to be a **path** or a **cycle** ✓ Along either, edges must **alternate** between M and N — two consecutive edges from the same matching would share a vertex ✗ An alternating cycle must therefore have **even** length.

> *This is the "does there exist odd cycles in H?" question on my page. Answer: **no** — an odd cycle would force two adjacent edges from the same matching, violating the matching property.*

So each component of H is: an **isolated vertex**, a **path**, or an **even cycle**.

**Claim 2.3 — some component has more N-edges than M-edges.**
Count component by component:

| component type | M vs N edges |
|---|---|
| isolated vertex | 0 = 0 — contributes equally |
| **even cycle** | alternates ⇒ **equal** |
| **even-length path** | starts and ends with different types ⇒ **equal** |
| **odd-length path** | one more of whichever type it starts *and* ends with |

Since |N| > |M| overall, at least one component must carry the surplus. By the table it can only be an **odd-length path whose end edges both belong to N** ✓

**Claim 2.4 — that component is an M-augmenting path.**
Its two end edges are in N, hence **not** in M. If an endpoint had an M-edge, that edge would lie in H and continue the path — so both endpoints are **unmatched by M** ✓ And its edges alternate M/N, i.e. alternate in/out of M ✓

**Combining Claims 2.1–2.4:** that component is an M-augmenting path ∎

> ⚠️ **A note in my page says** the surplus component "cannot form an N-augmenting path since N is assumed to be maximum" — careful, N was only assumed **bigger** than M, not maximum. The argument doesn't need N to be maximum; it only needs |N| > |M|. *(If you do take N maximum, the remark is a valid extra sanity check.)*

---

### Combining the lemmas

**Lemma 1 + Lemma 2** give the equivalence:

> ★ **A matching M is not maximum ⟺ there exists an M-augmenting path in G.**

## The algorithm that falls out

```
M ← ∅
while ∃ an M-augmenting path P:
        M ← (M ∖ P) + (P ∖ M)        # augment along P
return M
```

Each pass adds exactly one edge, so it halts after at most ⌊n/2⌋ rounds. Berge guarantees that when no augmenting path can be found, **M is maximum** — that is the whole reason the algorithm is correct.

---

## 5. Vertex covers, and the sandwich

> A subset **S ⊆ V(G)** is a **vertex cover** if for every edge e = {u,v} ∈ E(G), **S ∩ {u,v} ≠ ∅** — every edge has at least one endpoint in S.

### Values

| Graph | \|MVC\| |
|---|---|
| Pₙ | ⌊n/2⌋ |
| Cₙ | ⌈n/2⌉ |
| Star Sₙ | 1 |
| Kₙ | n−1 |
| Tree T | k |
| **K_{k,l}** | **min{k, l}** |

### ★ The sandwich: |MM| ≤ |MVC| ≤ 2·|MM|

**Claim 5.1 — |MM| ≤ |MVC| (lower half).**
Take a maximum matching M. Any vertex cover must cover **every edge of M**, so it contains at least one endpoint of each. The edges of M are **pairwise disjoint**, so those endpoints are |M| **distinct** vertices ✓ → also [[Lec 01 — Vertex Cover and Independent Set]] §3

**Claim 5.2 — |MVC| ≤ 2·|MM| (upper half).**
Take a **maximum** matching M and let **VC := V(M)** — *all* endpoints of M, so |V(M)| = 2|M|.

Is V(M) a vertex cover? Take any edge e = uv. If **neither** u nor v were in V(M), then M + e would be a bigger matching ✗ contradicting maximality. So at least one endpoint is in V(M) ✓

Hence V(M) is a vertex cover of size 2|MM|, giving |MVC| ≤ 2|MM| ✓

**Combining:**

$$|MM| \;\le\; |MVC| \;\le\; 2\,|MM|$$

### Both ends are tight

- **Lower tight:** any bipartite graph — by König (§6). E.g. Pₙ.
- **Upper tight:** **K₃**. |MM| = 1, |MVC| = 2 = 2·1 ✓ More generally a disjoint union of triangles.

> **Why this matters practically:** taking both endpoints of a maximum matching is the classic **2-approximation** for the NP-hard minimum vertex cover problem. Claim 5.2 *is* that algorithm's guarantee.

**Worked check on C₂ₙ:** |MM| = n and |MVC| = n ✓ equal (even cycle is bipartite).

---

## 6. ★ König's Theorem (1936)

> **Theorem (König).** If G is **bipartite**, then **|MM(G)| = |MVC(G)|**.

*(My page has "1936" and also "1736" — 1936 is König's; 1736 is Euler and Königsberg, an easy slip since the names look alike.)*

### The construction

Let (A, B) be the bipartition and let **M be a maximum matching**. Define, in this order:

| Set | Definition |
|---|---|
| **A₀** | vertices of **A** that are **unmatched** |
| **B₀** | vertices of **B** that are **unmatched** |
| **B₁ ⊆ B** | vertices reachable from **A₀** by **M-alternating paths** |
| **A₁** | the **matching partners** of B₁ |
| **B₂** | N(A₁) ∖ B₁ |
| **A₂** | the rest — A ∖ (A₀ ∪ A₁) |

```
        A                        B
   ┌──────────┐            ┌──────────┐
   │   A₀     │  unmatched │   B₀     │  unmatched
   │──────────│            │──────────│
   │   A₁     │◄── matched │   B₁     │  reachable from A₀
   │──────────│            │──────────│
   │   A₂     │            │   B₂     │  = N(A₁) ∖ B₁
   └──────────┘            └──────────┘
```

> ★ **Claim: B₁ ∪ A₂ is a vertex cover.**

### Proof of the Claim — three forbidden edge types

We must show no edge escapes B₁ ∪ A₂. The only edges that could escape run from **A₀ ∪ A₁** to **B₀ ∪ B₂**. Three cases, each ruled out.

**Claim 6.1 — no edge from A₁ to B₀.**
Suppose a₁ ∈ A₁ had an edge to some unmatched b₀ ∈ B₀. By definition a₁ is the matching partner of some vertex of B₁, which is reachable from A₀ by an M-alternating path. Extend that path through a₁ and out along the edge to b₀. Both ends — the A₀ start and the B₀ finish — are **unmatched**, so this is an **M-augmenting path** ✗ contradicting that M is maximum (Berge, §4) ✓

**Claim 6.2 — no edge from A₀ to B₂.**
Suppose a₀ ∈ A₀ had an edge to x ∈ B₂. Then x is reachable from A₀ by a one-edge M-alternating path, so by **the definition of B₁**, x should be in B₁ ✗ But x ∈ B₂ = N(A₁) ∖ B₁ ✓

**Claim 6.3 — no edge from A₁ to B₂.**
Suppose w ∈ A₁ had an edge to y ∈ B₂. Since w ∈ A₁, w is matched to some **z ∈ B₁**, and there is an M-alternating path **P** from A₀ to z. Now extend:

$$P \;+\; zw \;+\; wy$$

The edge **zw is in M**, and **wy is not**, so the alternation is preserved — this is an M-alternating path from A₀ reaching **y**. By the definition of B₁, that forces **y ∈ B₁** ✗ contradicting y ∈ B₂ ✓

**Combining 6.1–6.3:** every edge has an endpoint in **B₁ ∪ A₂**, so it is a vertex cover ∎

### Finishing the theorem

**Claim 6.4 — |A₂ ∪ B₁| = |M|.**

- Every vertex of **B₁** is matched — an unmatched B-vertex reachable from A₀ would be an augmenting path (Claim 6.1's argument) — and its partner lies in A₁.
- Every vertex of **A₂** is matched, since the unmatched A-vertices are exactly A₀, and A₂ excludes A₀.
- These use **different** M-edges: A₂-vertices are matched into B ∖ B₁ (a partner in B₁ would put them in A₁), while B₁-vertices are matched into A₁ ✓

So the cover uses one M-edge per vertex, no two sharing: **|B₁ ∪ A₂| = |M|** ✓

**Combining with the sandwich:**

$$|MVC| \;\le\; |B_1 \cup A_2| \;=\; |M| \;=\; |MM| \qquad\text{and}\qquad |MM| \le |MVC| \ \ \text{(Claim 5.1)}$$

Therefore **|MM| = |MVC|** in bipartite graphs ∎

> **Where bipartiteness was used:** the whole A/B layering. In K₃ the argument collapses — there are no "sides" to alternate between — and indeed |MM| = 1 < 2 = |MVC| there.

---

## 7. The open questions from class

### (a) Complete bipartite graphs

**Question:** for complete bipartite K_{|A|,|B|}, is |MM| = |MVC|?

**Yes**, and you can see it directly. Say |A| ≤ |B|. Every vertex of A can be matched to a private partner, so |MM| = |A|. And A itself covers every edge, so |MVC| ≤ |A|. With Claim 5.1:

$$|A| = |MM| \le |MVC| \le |A| \quad\Longrightarrow\quad |MM| = |MVC| = \min\{|A|,|B|\} \;✓$$

### (b) Is |MVC| = min{|A|, |B|} for *every* bipartite graph?

**No.** My page has a counterexample sketched; here it is precisely.

Take **A = {a, b, c, d, e}** and **B = {p, q, r, s, t}**, but put edges only from **a** and **b** into B:

```
 A:  a  b  c  d  e         only a and b have edges
     │╲ │╲                 c, d, e are isolated
 B:  p q r s t
```

Then **{a, b}** covers every edge, so |MVC| = 2 — but min{|A|,|B|} = 5 ✗

**The lesson:** min{|A|,|B|} is only an *upper bound*. Equality needs the graph to be **complete** bipartite (part (a)).

### (c) Is the smaller side always a minimum vertex cover?

**No** — the same counterexample. Both sides have size 5, but the minimum cover {a, b} has size 2 and is not a side at all.

### (d) ★ Is the bipartition unique in a **connected** bipartite graph?

**Yes** — unique up to swapping the two sides. *(This was left open on my page; here's the proof.)*

**Proof.** Fix any vertex **r**, and let (X, Y) be any bipartition with r ∈ X.

**Claim (d).1 — in a bipartite graph, all r–v paths have the **same parity** of length.**
Walking any path alternates sides. So a path of **even** length ends on r's side, and a path of **odd** length ends on the other side. Since a vertex sits on exactly one side, every r–v path has the same parity ✓

**Claim (d).2 — the side of v is forced.**
By Claim (d).1, v ∈ X exactly when some (equivalently every) r–v path has even length. **Connectedness** guarantees at least one such path exists ✓

So once you decide which side r goes on, **every other vertex's side is determined** — the bipartition is unique up to swapping the names X and Y ∎

> ⚠️ **Connectedness is essential.** For a disconnected graph, each component can be flipped independently. Two disjoint edges have **four** different bipartitions.

---

## Takeaways

1. **|MVC| = n − |MIS|** — the table's third column is Gallai's identity in disguise.
2. **A leaf's edge lies in some maximum matching** — proved by an **exchange argument**, the same shape as the MIS leaf claim.
3. **Augment along an augmenting path** with M △ P: the swap gains exactly one edge.
4. **Berge** is the whole theory of matching algorithms: no augmenting path ⟺ maximum.
5. **M ∪ N has max degree 2**, so it splits into alternating paths and even cycles. This decomposition is the engine of Lemma 2 — and it reappears throughout matching theory.
6. **|MM| ≤ |MVC| ≤ 2|MM|**: the lower half is disjointness, the upper half is "take both endpoints" — which is the standard 2-approximation for vertex cover.
7. **König** = the lower half becomes equality when bipartite. The proof **constructs** the cover as B₁ ∪ A₂ from alternating reachability out of the unmatched vertices A₀.
8. **min{|A|,|B|} is only an upper bound** on |MVC| — equality needs complete bipartite.
9. **Connected + bipartite ⇒ unique bipartition** (up to swapping).

---

## Doubts / to revisit

- [ ] "No. of maximum ind. set = 3^(n/3)" → Moon–Moser counts **maximal** independent sets, and it's an upper **bound on the count**, not a size.
- [ ] In Lemma 2 my page says N is "assumed to be maximum" — only **|N| > |M|** is needed.
- [ ] My page has both "1936" and "1736" for König — **1936** is right; 1736 is Euler/Königsberg.
- [ ] The König construction here uses A₀/B₁/A₁/B₂/A₂; my NPTEL note [[Lec 02 — König's Theorem and Hall's Theorem]] uses S/T reachability. **Same proof, different labels** — worth reading both once.
- [ ] Class asked what graphs with Δ ≤ 2 look like — answer: disjoint unions of paths and cycles. Used in Claim 2.2.
