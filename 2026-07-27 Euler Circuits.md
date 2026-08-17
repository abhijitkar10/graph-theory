---
tags: [academics, graph-theory, lecture]
date: 2026-07-27
seq: 3
class: 2
---

# 3 · 2026-07-27 — Euler Circuits

**◀ Previous:** [[2026-07-24 Long Path Theorem]]  ·  **Hub:** [[Graph Theory]]  ·  **Next ▶** [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]]

**Covered:** walks/trails/circuits, components, Euler's Theorem and its two lemmas (both proved in full), contrapositives, the Königsberg bridge problem, a note on Hamiltonian cycles.

---

## 0. The vocabulary — get this exactly right

These four words look similar and mean different things. The whole topic collapses into confusion if they blur, so here they are side by side.

| Term | Definition | Repeats allowed? |
|---|---|---|
| **Walk** | any sequence of vertices where consecutive ones are joined by an edge | vertices ✓ edges ✓ |
| **Trail** | a walk with **no repeated edges** | vertices ✓ edges ✗ |
| **Path** | a walk with **no repeated vertices** | vertices ✗ edges ✗ |
| **Circuit** | a **closed trail** — a trail whose start and end are the same vertex | vertices ✓ edges ✗ |

So: **trail = walk without repeated edges**, and **circuit = trail with the same start and end point**. A circuit may pass through the *same vertex* several times; it just must never reuse an *edge*.

```
    a ——— b
    |  ╱  |          a → b → c → a → d → c is a TRAIL
    | ╱   |          (vertex a and c repeat, but no edge repeats)
    d ——— c
```

### Component

> A **component** is a **maximal connected subgraph**.

*Maximal* in the sense from [[2026-07-24 Preliminaries]] §5: you cannot add any more vertices to it and keep it connected.

> A component is **trivial** if it has **no edges** — i.e. it is a single isolated vertex.
> Otherwise it is **non-trivial**.

```
 ┌────────────┐   ┌──────┐
 │  a——b——c   │   │ d——e │      ●  f
 └────────────┘   └──────┘
  non-trivial     non-trivial   trivial
```

This graph has **2 non-trivial components** and 1 trivial one.

### Euler circuit

> An **Euler circuit** is a circuit that contains **all the edges** of G.

In plain terms: **draw the whole graph in one continuous pen stroke, never lifting the pen, never retracing an edge, and finish where you started.**

> ⚠️ Why "at most one non-trivial component" and not simply "connected": isolated vertices have **no edges**, so an Euler circuit doesn't need to visit them. They're allowed to float around freely. Only the *edge-carrying* part has to be in one piece.

---

## ★ Euler's Theorem

> **There exists an Euler circuit in G if and only if G has at most one non-trivial component and every vertex in G has even degree.**

*(My notes wrote "every vertex in the graph G has at most one non-trivial component" — that's a slip; it's **G** that has at most one non-trivial component.)*

"If and only if" means we owe **two** proofs, one in each direction. Those are Lemma 1 and Lemma 2.

| | Direction | Name |
|---|---|---|
| ⇒ | Euler circuit **exists** ⇒ conditions hold | **Lemma 1** (the easy half) |
| ⇐ | conditions hold ⇒ Euler circuit **exists** | **Lemma 2** (the hard half) |

---

## Lemma 1 — the necessary direction

> **If G has an Euler circuit, then G has at most one non-trivial component and every vertex in G has even degree.**

### Proof

Let **C** be an Euler circuit of G.

> **Structure:** three claims — (a) the components, (b) non-start vertices, (c) the start vertex — then combine.

#### Claim (a): at most one non-trivial component

A circuit is a single continuous journey. It never teleports — every step crosses an edge. So **C stays entirely inside the connected component where it starts.**

Now, C must contain **every** edge of G (that's what "Euler" means). If G had **two** non-trivial components, each would contain at least one edge, and C would have to contain edges from **both**. But C can't reach across from one component to the other. **Contradiction.**

Therefore G has **at most one** non-trivial component. ✓

#### Claim (b) and (c): every vertex has even degree

Here's the key observation:

> **Every time the circuit visits a vertex, it uses exactly 2 edges — one to come *in*, one to go *out*.**

So we can **pair up** the edges at each vertex: each visit consumes one in-edge and one out-edge, one pair.

**Case 1 — a vertex v that isn't the start.** Suppose the circuit passes through v exactly **ℓ** times. Each visit uses 2 edges, so the circuit uses **2ℓ** edges at v. Because the circuit is an *Euler* circuit it contains **all** edges of G, so *every* edge touching v is among these. Hence

$$\deg(v) = 2\ell \quad \text{— even} \;✓$$

**Case 2 — the starting vertex v₀.** This is the case my notes trailed off on. The journey **leaves** v₀ at the very beginning and **returns** to it at the very end. Those two edges — the **starting edge** and the **ending edge** — are unmatched at first glance, but since the circuit is *closed* (it ends where it began), we simply **pair the starting edge with the ending edge**. That's one more pair.

If the circuit additionally passes *through* v₀ in the middle **ℓ** times, those contribute 2ℓ edges, plus the start/end pair contributes 2:

$$\deg(v_0) = 2\ell + 2 = 2(\ell+1) \quad \text{— even} \;✓$$

**Case 3 — an isolated vertex.** Degree 0, which is even ✓

Every vertex has even degree. ∎

> **Intuition to keep:** an Euler circuit "consumes" edges at a vertex strictly two at a time. Anything left over would strand you. An odd-degree vertex always leaves you stuck with an unused edge and no way out.

---

## Lemma 2 — the sufficient direction

> **If G has at most one non-trivial component and every vertex in G has even degree, then G has an Euler circuit.**

This is the harder half. Proof is by **induction on the number of edges** (as flagged in class: *"induction on no. of edges"*).

> ⚠️ **There is a second, shorter proof of this lemma** — the **maximal trail / extremal argument** given in the 29 July class. See [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]] Part A. It avoids the fiddly component-splicing in Step 4 below. Worth knowing both.

### Stepping stone we already have

From [[2026-07-24 Preliminaries]] §6, **Lemma B**:

> **δ(G) ≥ 2 ⇒ G contains a cycle C.**

*(This is exactly the "δ ≥ 2 ⇒ ∃ a cycle C in G" line at the top of my page.)*

### Proof

**Induction on m, the number of edges.**

#### Base case: m = 0

There are no edges. The "empty circuit" — stand at a vertex and don't move — trivially contains all 0 edges. ✓

#### Inductive hypothesis

Assume the lemma holds for every graph with **fewer than m** edges.

#### Inductive step

Let G have **m ≥ 1** edges, all degrees even, at most one non-trivial component. Call that non-trivial component **H** (it exists since m ≥ 1).

**Step 1 — find a cycle.** Every vertex of H has degree ≥ 1 (it's in a connected component with edges) and **even**, so degree ≥ **2**. Thus δ(H) ≥ 2, and by the stepping stone **H contains a cycle C**.

**Step 2 — rip the cycle out.** Let **G′ = G − E(C)** (delete the cycle's *edges*, keep all vertices).

> **Degrees stay even.** A cycle touches each of its vertices exactly **twice** (one edge in, one edge out). So every vertex loses **either 0 or 2** from its degree. Even − 0 = even, even − 2 = even ✓

And G′ has **fewer edges** than G, so the inductive hypothesis is available.

**Step 3 — the "2 cases" from class.** After deleting C, is G′ still in one piece?

- **Case (i): G′ is connected** (at most one non-trivial component). The hypothesis applies directly.
- **Case (ii): G′ is not connected** — deleting the cycle may have shattered H into **several** non-trivial components D₁, D₂, …, Dₜ.

Case (ii) is the reason we can't apply induction naively to G′ as a whole. **The fix:** apply the inductive hypothesis to **each component separately**. Each Dₛ is connected and has all even degrees, and has fewer than m edges, so **each Dₛ has its own Euler circuit**.

**Step 4 — every piece touches the cycle.** *(The crucial gluing fact.)*

> **Claim:** every non-trivial component D of G′ shares at least one vertex with C.

*Why:* pick any vertex **u** in D. Since H was **connected**, there is a path in H from u to some vertex of C. Walk along it and let **x** be the **first** vertex on this path that lies on C. Every edge before reaching x joins two vertices that are **not on C** — so none of those edges belong to C, meaning they all survive into G′. Hence u and x are connected **within G′**, so **x ∈ D**. And x ∈ V(C). ✓

**Step 5 — splice everything into one circuit.** Now traverse **C**. Whenever you arrive at a vertex that belongs to some component Dₛ you haven't handled yet, **take a detour**: run Dₛ's entire Euler circuit (it starts and ends at that very vertex, so you come back to where you left off), then carry on along C.

```
        ┌──── detour through D₁'s Euler circuit ────┐
        │                                            │
   C:  ─●──────────●─────────────●──────────────────●─ …
                   │             │
                   └── detour ───┘  through D₂'s Euler circuit
```

The result is a **single closed trail** that uses:
- every edge of **C** (walking the cycle once), and
- every edge of every **Dₛ** (each detour is an Euler circuit of that piece),

which together are **all the edges of G** — each exactly once. That is an **Euler circuit** of G. ∎

---

## Putting it together

**Lemma 1 + Lemma 2 = Euler's Theorem.** Lemma 1 proves ⇒, Lemma 2 proves ⇐, so the "if and only if" is established. ∎

---

## The contrapositive — how to actually *use* the theorem

Lemma 1 has the logical shape

$$P \implies (Q \wedge R)$$

where **P** = "G has an Euler circuit", **Q** = "at most one non-trivial component", **R** = "every vertex has even degree".

Its contrapositive is

$$\neg(Q \wedge R) \implies \neg P$$

and by **De Morgan's law**, ¬(Q ∧ R) = ¬Q ∨ ¬R, giving

$$\neg Q \;\vee\; \neg R \implies \neg P$$

*(My notes wrote this as `(Q∧R)′ ⇒ P′`, then `Q′ ∨ R′ ⇒ P′` — same thing.)*

**Read out in words:**

> **If G has more than one non-trivial component, OR at least one vertex of G has odd degree, then G does NOT have an Euler circuit.**

Note how the **AND flipped into an OR**. That's De Morgan, and it's the whole practical value: to rule out an Euler circuit you only need to catch **one** offending vertex.

### Königsberg — "Bridge tour is not possible"

The classic application. Four land masses (A, B, C, D) joined by seven bridges; the question was whether you could walk a route crossing every bridge exactly once and return home — i.e. an **Euler circuit**.

```
        A
       /|\
      / | \        C ══════ D      (multiple bridges
     /  |  \        \      /        between the same
    B---+---+        \    /         land masses)
                       ...
```

Degrees in the Königsberg graph: **3, 3, 3, 5** — every single one is **odd**.

By the contrapositive, one odd-degree vertex is already fatal. Here there are four. So **no Euler circuit exists — the bridge tour is impossible.** ∎

> This is the problem Euler solved in 1736, generally taken as the birth of graph theory.

---

## Aside — Hamiltonian cycles and TSP

Class contrasted Euler circuits with Hamiltonian ones. The distinction is worth pinning down:

| | **Euler circuit** | **Hamiltonian cycle** |
|---|---|---|
| Must cover | every **edge** exactly once | every **vertex** exactly once |
| Test | easy — just check degrees | **NP-complete** |
| Verdict | solved (Euler's Theorem) | no known efficient characterisation |

**"Best way to check if Hamiltonian cycle?"** — my notes list guesses (`ⁿC_m`, `n!`, …). The honest answer:

- **Brute force:** try every ordering of vertices → about **n!** checks. Hopeless beyond n ≈ 15.
- **Best known exact algorithm:** Held–Karp dynamic programming, **O(2ⁿ · n²)** — still exponential, but far better than n!.
- **The travelling salesman problem (TSP)** is the optimisation cousin (cheapest Hamiltonian cycle) and is **NP-complete** in its decision form.

The striking lesson: **"cover every edge" is easy; "cover every vertex" is hard.** Two questions that sound like near-mirror images sit on opposite sides of the tractability line.

---

## Takeaways

1. **Trail** = no repeated *edges*. **Path** = no repeated *vertices*. **Circuit** = closed trail. Keep them separate.
2. **Euler circuit ⟺ ≤1 non-trivial component AND all degrees even.**
3. The engine of Lemma 1: **a visit to a vertex burns exactly 2 edges** — so degrees pair up and must be even.
4. The engine of Lemma 2: **pull out a cycle, recurse on what's left, then splice the pieces back in as detours.**
5. Deleting a cycle's edges **preserves even-ness** (each vertex loses 0 or 2) — that's what keeps the induction alive.
6. **De Morgan matters:** the useful form of the theorem flips AND into OR, so a *single* odd vertex kills the whole thing.
7. Isolated vertices are harmless — an Euler circuit only owes a visit to **edges**, not vertices.

---

## Doubts / to revisit

- [ ] Statement typo in my notes: "every vertex in the graph G has at most one non-trivial component" → should be "**G** has at most one non-trivial component".
- [ ] The Case (ii) gluing step (Step 4) is the subtle one — re-read if Lemma 2 feels shaky.
- [ ] Hamiltonian cycle proof techniques — flagged in class for later.
