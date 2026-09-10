---
tags: [academics, graph-theory, plan]
type: plan
exam: 2026-09-12
---

# Exam plan, four days to 12 September

Hub: [[Graph Theory]] · Cram sheet: [[Revision Sheet]] · Distilled: [[Takeaways]]

Covers the nine class notes from 24 July to 19 August. Nothing after that date is included.

Every instruction below links to the exact section. Click through rather than hunting.

## The honest position

Nine notes, about 16,000 words of proof. One careful read is roughly six hours, and reading is not the same as being able to reproduce. Four days at four focused hours gives sixteen hours, which is enough for one proper pass plus one recall pass plus problems, but only if you do not try to hold everything at the same depth.

## Three tiers

Tier one, must be able to write out cold.

- [[2026-07-27 Euler Circuits#Lemma 1, the easy half|Euler, Lemma 1]] and [[2026-07-27 Euler Circuits#Lemma 2, the hard half|Euler, Lemma 2]]
- [[2026-07-29 Matchings 2 — Berge and König#Berge's theorem|Berge's theorem]]
- [[2026-07-29 Matchings 2 — Berge and König#König's theorem|König]], or the shorter [[2026-08-10 König by Induction, Hall, and Factors#A third proof of König|induction proof]]
- [[2026-08-10 König by Induction, Hall, and Factors#Hall's theorem|Hall's theorem]]
- [[2026-08-19 Tutte's 1-Factor Theorem#What we are proving|Tutte's statement]] plus [[2026-08-19 Tutte's 1-Factor Theorem#The hard direction|the three moves]]

Tier two, state and use, sketch the idea.

- [[2026-07-24 Long Path Theorem#What we are proving|Long path theorem]]
- [[2026-07-24 Preliminaries#What high minimum degree buys you|The δ at least k family]]
- [[2026-07-24 Preliminaries#Large density forces a dense subgraph|Density gives a dense subgraph]]
- [[2026-07-29 Matchings 2 — Berge and König#Vertex covers, and the sandwich|The sandwich]]
- [[2026-08-19 Tutte's 1-Factor Theorem#Petersen's theorem|Petersen]]
- [[2026-08-10 König by Induction, Hall, and Factors#Factors|The 2 factor theorem]]

Tier three, recognise and quote.

- [[2026-07-29 Matchings 2 — Berge and König#The four parameters and how they pair up|Gallai identities]]
- [[Revision Sheet#2. Numbers to know cold|Standard values of α, β and α′]]
- [[Tutorial 1#Question 1, the hypercube|Planarity bounds]]

## How to study, not just what

Reading a proof and understanding it feels like learning and is not. The thing that works is retrieval. For every proof in tier one and two:

1. Read the section once, slowly, until each step makes sense.
2. Close it. On blank paper write the statement, then the proof, from memory.
3. Reopen and mark every place you were vague, wrong, or stuck.
4. Come back to the marked spots the next day, not the same day.

Step 2 is uncomfortable and is the part that works.

## Monday 8 September, foundations and the extremal method

Read [[2026-07-24 Preliminaries]] and [[2026-07-24 Long Path Theorem]].

From memory afterwards, write out:

- [[2026-07-24 Preliminaries#Counting degrees|the handshake lemma]], and why the number of odd degree vertices is even
- [[2026-07-24 Preliminaries#What high minimum degree buys you|the three δ at least k results]]
- [[2026-07-24 Preliminaries#Maximal is not the same as maximum|why maximal is enough]] where longest would do
- [[2026-07-24 Preliminaries#Minimum degree three forces an even cycle|why δ at least 3 forces an even cycle]], including the odd plus odd is even step
- [[2026-07-24 Long Path Theorem#Second case: k is at most n−2|the long path theorem]], the whole second case

Then do [[Assignment 1#Q9 + Path or cycle of length at least min 2δ(G), n|Assignment Q9]], [[Assignment 1#Q12 − Every 2-connected graph contains a cycle|Q12]], [[Assignment 1#Q20 − Every tree T has at least Δ(T) leaves|Q20]] and [[Assignment 1#Q21 A tree with no degree-2 vertex has more leaves than other vertices|Q21]]. Q9 is the long path theorem with a small upgrade, so it tests whether you own that proof.

Target four hours. If you overrun, read [[2026-07-24 Preliminaries#Trees|Trees]] and [[2026-07-24 Preliminaries#Bipartite graphs|Bipartite graphs]] only, since both come back tomorrow.

## Tuesday 9 September, Euler and trees

Read [[2026-07-27 Euler Circuits]] and [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]].

From memory:

- [[2026-07-27 Euler Circuits#What we are proving|the statement]], then [[2026-07-27 Euler Circuits#Lemma 1, the easy half|Lemma 1]] in full
- [[2026-07-27 Euler Circuits#Lemma 2, the hard half|Lemma 2]] by maximal trail, both halves
- [[2026-07-27 Euler Circuits#Using the theorem in practice|why the and becomes an or]], and what that does for [[2026-07-27 Euler Circuits#Konigsberg|Konigsberg]]
- [[2026-07-24 Preliminaries#Trees|the four tree characterisations]]
- [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees#Part C, largest independent set in a tree|the exchange argument for leaves]]

Then [[Assignment 1#Q19 Prove Theorem 1.5.1 (characterisations of a tree)|Assignment Q19]] and [[Assignment 1#Q22 Forest exchange property|Q22]], and revisit yesterday's marked spots.

Target four hours. Euler is the cheapest tier one theorem to secure, so do not leave it half done.

## Wednesday 10 September, the matchings core

The biggest block and the most likely to carry the heaviest question.

Read [[2026-07-29 Matchings 2 — Berge and König]] and [[2026-08-10 König by Induction, Hall, and Factors]].

From memory:

- [[2026-07-29 Matchings 2 — Berge and König#The four parameters and how they pair up|the four parameters and both Gallai identities]]
- [[2026-07-29 Matchings 2 — Berge and König#Matching number never exceeds cover number|why matching is at most cover]], and [[2026-07-29 Matchings 2 — Berge and König#Vertex covers, and the sandwich|why endpoints give at most twice]]
- [[2026-07-29 Matchings 2 — Berge and König#Berge's theorem|Berge]], in particular the M union N decomposition
- [[2026-07-29 Matchings 2 — Berge and König#König's theorem|König]] by whichever proof you find easiest
- [[2026-08-10 König by Induction, Hall, and Factors#Hall's theorem|Hall]], and where the violating set comes from
- [[2026-08-10 König by Induction, Hall, and Factors#Regular bipartite graphs|k regular bipartite has a perfect matching]]

Then write the table of α, β and α′ for paths, cycles, stars, complete and complete bipartite graphs from memory, and check against [[Revision Sheet#2. Numbers to know cold|the numbers section]].

Target five hours. Take the extra hour from somewhere. This day matters most.

## Thursday 11 September, the hard theorems and full revision

Read [[2026-08-10 Matchings in Bipartite Graphs]] and [[2026-08-19 Tutte's 1-Factor Theorem]].

From memory:

- [[2026-08-10 Matchings in Bipartite Graphs#The proof|the universal vertex theorem]], and [[2026-08-10 Matchings in Bipartite Graphs#Why the question is interesting|why odd cycles are the only obstruction]]
- [[2026-08-19 Tutte's 1-Factor Theorem#The easy direction|Tutte's easy direction]] in full, and [[2026-08-19 Tutte's 1-Factor Theorem#The hard direction|the three moves]] of the hard one
- [[2026-08-19 Tutte's 1-Factor Theorem#Petersen's theorem|Petersen]], including where bridgelessness is used

Then work [[Tutorial 1]] straight through without looking:

- [[Tutorial 1#Question 1, the hypercube|Q1 hypercube]]
- [[Tutorial 1#Question 2, girth five forces size|Q2 girth five]]
- [[Tutorial 1#Question 3, an induced path of length two|Q3 induced path]]
- [[Tutorial 1#Question 4, two longest paths meet|Q4 longest paths meet]]
- [[Tutorial 1#Question 5, shortest paths are induced|Q5 shortest is induced]]
- [[Tutorial 1#Question 6, intervals with pairwise overlaps|Q6 Helly]]

These are the closest thing you have to exam questions, since they came from your own tutorial.

Finish with one pass of [[Revision Sheet]], marking anything still unfamiliar.

Target five hours.

## Friday 12 September, exam day

Read only [[Takeaways]], or the PDF version. Do not open a proof for the first time on exam morning.

If you have twenty minutes, spend them on [[Takeaways#Traps|the traps]] rather than the theorems. Those are errors you have actually made.

## If you fall behind

Cut in this order.

1. Drop the [[Assignment 1]] questions. [[Tutorial 1]] is closer to the exam.
2. Drop [[2026-08-10 König by Induction, Hall, and Factors#Factors|the 2 factor theorem]] and [[2026-08-19 Tutte's 1-Factor Theorem#Petersen's theorem|Petersen]]. Attractive results, edge of the syllabus.
3. Keep one proof of König and drop the others.

Do not cut [[2026-07-29 Matchings 2 — Berge and König#Berge's theorem|Berge]] or [[2026-07-27 Euler Circuits#Lemma 2, the hard half|Euler]]. They are cheap and everything leans on them.

## Checklist

- [ ] Mon: [[2026-07-24 Preliminaries]], [[2026-07-24 Long Path Theorem]], Assignment Q9 Q12 Q20 Q21
- [ ] Tue: [[2026-07-27 Euler Circuits]], [[2026-07-29 Euler by Extremal Argument, Matchings, MIS in Trees]], Assignment Q19 Q22
- [ ] Wed: [[2026-07-29 Matchings 2 — Berge and König]], [[2026-08-10 König by Induction, Hall, and Factors]], parameter table
- [ ] Thu: [[2026-08-10 Matchings in Bipartite Graphs]], [[2026-08-19 Tutte's 1-Factor Theorem]], [[Tutorial 1]] in full, [[Revision Sheet]]
- [ ] Fri: [[Takeaways]] only
