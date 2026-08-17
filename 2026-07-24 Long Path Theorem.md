---
tags: [academics, graph-theory, lecture]
date: 2026-07-24
seq: 2
class: 1
---

# 2 · 2026-07-24 — Long Path Theorem

**◀ Previous:** [[2026-07-24 Preliminaries]]  ·  **Hub:** [[Graph Theory]]  ·  **Next ▶** [[2026-07-27 Euler Circuits]]

**Covered:** minimum degree, longest-path argument, pigeonhole, folding a path into a cycle.

> This was set in class as: *"Exercise: Any connected simple graph has a path of length at least min{2δ(G), n−1}."* Split into its own note because the proof is long.

---

## Symbols used today

| Symbol | Meaning |
|---|---|
| **n** | number of vertices in the graph |
| **δ(G)** | *minimum degree* — the smallest number of edges touching any single vertex (the problem sheet wrote this as D(G)) |
| **length of a path** | number of **edges** in it. A path on m vertices has length m−1. Example: v₀ v₁ v₂ v₃ v₄ has 5 vertices, length 4 |
| **u ~ v** | "u is adjacent to v", i.e. there is an edge between them |
| **N(v)** | the set of neighbours of v |

---

## Theorem

> Any **connected simple** graph G has a path of length ≥ min{2δ(G), n−1}.

---

## The one big idea

Look at the **longest path** in the graph. Its two **endpoints are trapped** — they cannot reach any vertex that isn't already on the path. (If an endpoint had a neighbour outside, you could tack it on and get a *longer* path, contradicting "longest".)

So every neighbour of each endpoint is crammed onto the path itself. Each endpoint has **at least δ neighbours**, so the path must be long enough to hold them all. That crowding is what forces the bound.

---

## Setup

Let **P = v₀ v₁ v₂ … vₖ** be a **longest path** in G.
- Its length is **k** — this is the number we want to bound.
- It has **k + 1 vertices** (one more than k, because we start counting at v₀).

---

**Structure of the proof.** Six small claims, each proved on its own, then combined at the end:

| | Claim |
|---|---|
| **1** | both endpoints are *trapped* — all their neighbours lie on P |
| **2** | the two neighbour-lists A and B sit inside a box of size k |
| **3** | if the path is short, A and B must **overlap** (pigeonhole) |
| **4** | that overlap **folds P into a cycle** through all k+1 vertices |
| **5** | if k ≤ n−2, some vertex is **off** the cycle |
| **6** | that outside vertex builds a **longer path** — the contradiction |

---

## Claim 1 — The trapped-endpoint fact

> **Claim 1.** Every neighbour of v₀ lies among v₁,…,vₖ. Every neighbour of vₖ lies among v₀,…,vₖ₋₁.

**Why?** Suppose v₀ had a neighbour **u NOT on the path**. Since u ~ v₀, stick u onto the front:

$$u \to v_0 \to v_1 \to \cdots \to v_k$$

Is this a valid path? A path just needs **no repeated vertices**. The old part has no repeats, and u is brand new (we assumed it's off the path) — so nothing repeats. It's a genuine path, with one extra vertex, so length **k+1**.

But P was the **longest** path (length k). You can't beat the longest. **Contradiction.** So no such u exists, and all of v₀'s neighbours are already on the path. Same argument at the vₖ end (append instead of prepend).

### ⚠️ This works ONLY at the two ends

You can only extend a path at its **ends**. An interior vertex like v₃ is already boxed in by v₂ and v₄ — if v₃ has a neighbour u off the path, the edge u–v₃ branches off the *middle*, and a path isn't allowed to fork. No contradiction, so **interior vertices may have neighbours anywhere.**

Example — the longest path is still v₀ v₁ v₂ v₃ (length 3), yet interior vertex v₂ has an outside neighbour u:

```
v0 — v1 — v2 — v3
           |
           u
```

This is exactly why the proof leans entirely on the two endpoints — they're the only vertices whose neighbourhoods we can fully pin down. And it's why the bound is **2δ**: *two* trapped endpoints, each contributing ≥ δ neighbours.

---

## Splitting into two cases

Every whole number k is either ≥ n−1 or ≤ n−2 (nothing in between), so these two buckets cover **every** possibility. This is a *proof by cases* — we are not deriving one from the other, just handling each situation separately.

### Case 1: k ≥ n − 1

A path can't have more than n vertices, so k = n−1. Then k ≥ n−1 ≥ min{2δ, n−1}. **Done.**

### Case 2: k ≤ n − 2

Here "k ≤ n−2" is the **assumption defining this case** — it is *given*, not derived. Working under it, we prove **k ≥ 2δ**.

Suppose for contradiction the path is **short**: k ≤ 2δ − 1, which means **2δ > k**.

---

## Claim 2 — Two lists of positions, both inside one box

> **Claim 2.** The two sets A and B defined below each have size ≥ δ, and **both live inside {1, 2, …, k}**.

Both lists live inside the "box" of positions **{1, 2, …, k}** (size k):

- **A** = { i : v₀ ~ vᵢ }.  Since v₀ has ≥ δ neighbours and all are on the path, **|A| ≥ δ**.
- **B** = { i : vₖ ~ vᵢ₋₁ }.  Likewise **|B| ≥ δ**.

### Why the "−1" in B?

Two reasons, both essential:

**(a) It aligns the two edges we need.** The cycle we're about to build needs two *crossing* shortcut edges: v₀ reaching **forward** to vᵢ, and vₖ reaching back to **vᵢ₋₁** — the vertex *one spot earlier*. Defining B with the shift means a single shared index i hands us both edges at once.

**(b) It puts both lists in the same box.** v₀'s neighbours sit at positions {1,…,k}, so A ⊆ {1,…,k}. But vₖ's neighbours sit at positions {0,…,k−1}; writing them as i−1 with i = j+1 slides them into {1,…,k} too. Now both lists live in the *same* box of size k, which is what pigeonhole needs.

---

## Claim 3 — Pigeonhole forces an overlap

> **Claim 3.** If k ≤ 2δ − 1, then A and B **share an index i**, giving the two edges v₀ ~ vᵢ and vₖ ~ vᵢ₋₁.

**The plain idea first (no graphs).** Imagine 4 boxes numbered 1,2,3,4. List A has 3 numbers from them; list B has 3 numbers from them. Could they share nothing? That would need 3+3 = **6 distinct numbers** stuffed into only **4 boxes** — impossible. So they **must** share a number.

**Our case:** A and B both live in a box of size k, and

$$|A| + |B| \;\ge\; \delta + \delta \;=\; 2\delta \;>\; k.$$

Sizes add to more than the box → they cannot stay separate → they **share an index i**. Unpacking what that shared i means:

- i ∈ A → **v₀ ~ vᵢ**
- i ∈ B → **vₖ ~ vᵢ₋₁**

Exactly the two crossing edges we wanted.

---

## Claim 4 — Those two edges fold P into a cycle

> **Claim 4.** Given v₀ ~ vᵢ and vₖ ~ vᵢ₋₁, there is a **cycle through all k+1 vertices** of P.

Using those two edges:

$$v_0 \to v_1 \to \cdots \to v_{i-1} \;\to\; v_k \to v_{k-1} \to \cdots \to v_i \;\to\; v_0$$

Walk forward to vᵢ₋₁, **jump** across to vₖ, walk *backward* to vᵢ, then **jump** back to v₀. This is a **cycle through all k+1 vertices** of the path.

### Concrete example

Path v₀ v₁ v₂ v₃ v₄ (k = 4, length 4). Suppose the extra edges **v₀~v₃** and **v₄~v₂** exist — note they *cross*, offset by one:

```
      ┌───────────────┐        v0—v3
      │               │
   v0 — v1 — v2 — v3 — v4
                │
                └───────┐      v4—v2
```

The stroll: v₀ → v₁ → v₂ (walk), v₂ → v₄ (jump), v₄ → v₃ (walk back), v₃ → v₀ (jump). Back where we started — a **cycle on all 5 vertices**:

```
        v0 —— v1
       /        \
      v3         v2
       \        /
        v4 ————
```

If instead v₄ had joined **v₃** (same vertex v₀ reaches, no offset), the reroute would leave a stuck end and not seal into a full cycle. **The offset-by-one is what makes the loop close.**

---

## Claim 5 — Some vertex lies off the cycle

> **Claim 5.** If k ≤ n−2, then at least one vertex **w** of G is not on the cycle.

**Someone is off the cycle.** The cycle has k+1 vertices. Since k ≤ n−2, adding 1 to both sides gives **k+1 ≤ n−1**. The graph has **n** vertices, so the cycle holds at most n−1 of them — **at least one vertex w is left out.**

> Numbers: if n = 6, then k ≤ 4, so the cycle seats at most 5. Six vertices, five seats → someone's standing. That's w.
> ```
> Graph's vertices:  ● ● ● ● ● ●   (6 total)
> On the cycle:      ● ● ● ● ●     (at most 5)
> Left out:                    ●  ← w
> ```

**This is the whole reason Case 2 exists.** In Case 1 the path uses all n vertices, the cycle swallows everything, and there'd be *no* outside vertex to grab ✓ *(Claim 5 proved.)*

---

## Claim 6 — That outside vertex builds a longer path

> **Claim 6.** Given a cycle through all k+1 vertices of P and a vertex off it, G contains a path of length **k+1**.

**Connectedness hands us an edge.** G is connected, so w isn't floating alone — following its connections inward, some cycle-vertex **vⱼ** has an edge to a vertex outside the cycle.

**Snip and extend.** A cycle has no loose ends — but cut **one** of the two cycle-edges at vⱼ and the ring pops open into a **path on all k+1 vertices, ending at vⱼ**. Now vⱼ is a loose end, and it's joined to the outside vertex, which is unused. Glue it on:

→ a path with **k+2 vertices**, i.e. **length k+1 > k** ✓ *(Claim 6 proved.)*

**A path longer than the longest path. Contradiction.**

### Concrete example (continuing)

Cycle v₀→v₁→v₂→v₄→v₃→v₀, and outside vertex w joined to v₂:

```
        v0 —— v1
       /        \
      v3         v2 —— w
       \        /
        v4 ————
```

Snip edge v₂–v₄ → path **v₂ v₁ v₀ v₃ v₄** (all 5 vertices, v₂ now an endpoint). Prepend w → **w v₂ v₁ v₀ v₃ v₄**: 6 vertices, **length 5 > 4**. Contradiction ✓

---

## Combining all six claims

| | what it gave us |
|---|---|
| **Claim 1** | endpoints trapped ⇒ their neighbours are stuck on P |
| **Claim 2** | so A and B are two big sets inside a box of size k |
| **Claim 3** | if k ≤ 2δ−1 they overlap ⇒ two crossing edges |
| **Claim 4** | crossing edges ⇒ a cycle on all k+1 vertices |
| **Claim 5** | k ≤ n−2 ⇒ a vertex w sits off that cycle |
| **Claim 6** | w ⇒ a path of length k+1 — **beating the longest path** ✗ |

The assumption "k ≤ 2δ−1" was false, so **k ≥ 2δ** in Case 2.

- Case 1 gives **k ≥ n−1**
- Case 2 gives **k ≥ 2δ**

Either way:

$$k \;\ge\; \min\{2\delta(G),\; n-1\}. \qquad \blacksquare$$

---

## Sanity checks

- **Cycle Cₙ:** δ = 2, longest path has length n−1. Need n−1 ≥ min{4, n−1} ✓
- **Complete graph Kₙ:** δ = n−1, longest path n−1 = min{2(n−1), n−1} ✓

---

## Takeaways

1. **"Longest path" is a powerful assumption** — it traps both endpoints, forcing all their edges back onto the path.
2. Only the **two endpoints** are trapped; interior vertices are free.
3. **Two crossing shortcut edges** fold a path into a full cycle.
4. A **cycle** is better than a path here: snipping it open frees an endpoint you can extend.
5. Pigeonhole = *two lists in a box, sizes summing past the box size, must overlap.*

---

## Doubts / to revisit

- [ ] Where exactly this sits in West (PDF text layer is garbled; it's a Ch.1 exercise on degree & paths — also in Bondy & Murty)
