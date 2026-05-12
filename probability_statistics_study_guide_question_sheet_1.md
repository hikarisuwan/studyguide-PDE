# MATE50001.5 Probability & Statistics — Comprehensive Study Guide

## How to use this guide

This guide is written in a **problem → method → solution → pattern** style. It combines the lecture-note concepts with Question Sheet 1 and the worked solutions already discussed. The goal is not just to give answers, but to help you recognize the pattern behind each type of question.

---

# Part 1 — Probability language and set notation

## 1.1 Trial, outcome, sample space, and event

### Core idea
Probability starts with a **trial**. A trial is a well-defined process with uncertain result before it happens and a definite result afterwards.

Examples:

- Throwing a die.
- Drawing a card.
- Rolling three dice.
- Dealing a poker hand.
- Catching fish from a lake.

The result of the trial is called an **outcome**.

The set of all possible outcomes is the **sample space**, written as:

\[
\Omega
\]

An **event** is any subset of the sample space.

### Problem type
> Given a sample space and events, identify the event described by set notation.

### Example
If:

\[
\Omega=\{1,2,3,4,5,6\}
\]

and event \(A\) is “the number is even,” then:

\[
A=\{2,4,6\}
\]

The event \(A\) is a subset of \(\Omega\).

---

## 1.2 Venn diagram notation

### Symbols you must know

| Symbol | Meaning | Plain English |
|---|---|---|
| \(\Omega\) | sample space | everything possible |
| \(A\) | event A | outcomes inside A |
| \(A^c\) or \(\bar A\) | complement of A | not A |
| \(A\cap B\) | intersection | A and B |
| \(A\cup B\) | union | A or B or both |
| \(A\setminus B\) | difference | A but not B |
| \(\varnothing\) | empty set | nothing |
| \(\bar\Omega\) | complement of the sample space | nothing, so \(\varnothing\) |

### Key translations

\[
A\cap B = \text{in both A and B}
\]

\[
A\cup B = \text{in A or B, including overlap}
\]

\[
A\setminus B = A\cap B^c = \text{in A but not in B}
\]

\[
A^c = \Omega\setminus A = \text{everything not in A}
\]

\[
A\cap A^c=\varnothing
\]

\[
A\cup A^c=\Omega
\]

\[
\bar\Omega=\varnothing
\]

---

# Part 2 — Question Sheet 1, Questions 1–2: Venn diagram problems

## 2.1 Given diagram information

From the Question Sheet 1 diagram:

\[
\Omega=\{1,2,3,4,5,6,7,8,9,10\}
\]

The events are:

\[
A=\{1,3,4,7,10\}
\]

\[
B=\{2,5,7\}
\]

\[
C=\{5,6,7,10\}
\]

The regions are:

| Region | Outcomes |
|---|---|
| A only | \(\{1,3,4\}\) |
| B only | \(\{2\}\) |
| C only | \(\{6\}\) |
| A and B and C | \(\{7\}\) |
| A and C but not B | \(\{10\}\) |
| B and C but not A | \(\{5\}\) |
| Outside all three | \(\{8,9\}\) |

---

## 2.2 Problem: identify events from the diagram

### (a) \(A\)

\[
A=\{1,3,4,7,10\}
\]

### (b) \(B\)

\[
B=\{2,5,7\}
\]

### (c) \(A\cap B\)

This means in both A and B.

\[
A\cap B=\{7\}
\]

### (d) \(A\cap B\cap C\)

This means in all three sets.

\[
A\cap B\cap C=\{7\}
\]

### (e) \(A\cap B\setminus C\)

This means in A and B, but not C.

Since the only outcome in \(A\cap B\) is 7, and 7 is also in C:

\[
A\cap B\setminus C=\varnothing
\]

### (f) \(A\cap C\setminus B\)

This means in A and C, but not B.

\[
A\cap C=\{7,10\}
\]

Remove the part in B. Since 7 is in B but 10 is not:

\[
A\cap C\setminus B=\{10\}
\]

### (g) \(A\setminus B\)

This means in A but not B.

\[
A=\{1,3,4,7,10\}
\]

Remove 7 because it is in B.

\[
A\setminus B=\{1,3,4,10\}
\]

### (h) \(A\cup B\)

This means in A or B or both.

\[
A\cup B=\{1,2,3,4,5,7,10\}
\]

### (i) \(B\cup B\)

Unioning a set with itself changes nothing.

\[
B\cup B=B=\{2,5,7\}
\]

### (j) \(A\cup \bar B\cup C\)

This means in A, or not in B, or in C.

First:

\[
B=\{2,5,7\}
\]

So:

\[
\bar B=\Omega\setminus B=\{1,3,4,6,8,9,10\}
\]

Then:

\[
A\cup \bar B\cup C=\{1,3,4,5,6,7,8,9,10\}
\]

The only missing outcome is 2, because 2 is in B only and not in A or C.

### (k) \(\Omega\setminus A\)

This means everything not in A.

\[
\Omega\setminus A=\{2,5,6,8,9\}
\]

---

## 2.3 Pattern recognition for Venn diagram questions

When you see:

### Pattern 1: \(A\cap B\)
Think: “overlap only.”

### Pattern 2: \(A\cup B\)
Think: “everything in either set, but do not double-count overlap.”

### Pattern 3: \(A\setminus B\)
Think: “start with A, then remove anything also in B.”

### Pattern 4: \(A^c\)
Think: “everything outside A but still inside \(\Omega\).”

### Pattern 5: \(A\cap B\setminus C\)
Think: “first find A and B, then remove C.”

### Pattern 6: \(\Omega\setminus A\)
Think: “not A.”

---

## 2.4 Equivalent-event problem

The list in Question 2 includes:

\[
A,\ \varnothing,\ A\cup A^c,\ A\setminus B,\ \Omega\setminus(B\cap C\setminus A),\ \bar\Omega,\ \Omega,\ A\cap \bar B,\ [B\cap C\cap A^c]^c,\ A\cap A^c
\]

### Equivalent groups

#### Group 1: empty events

\[
\varnothing=\bar\Omega=A\cap A^c
\]

Reason: \(\Omega\) contains everything possible, so its complement contains nothing. Also, nothing can be both in A and not in A.

#### Group 2: whole sample space

\[
A\cup A^c=\Omega
\]

Reason: A plus not-A covers all possible outcomes.

#### Group 3: A but not B

\[
A\setminus B=A\cap \bar B
\]

Reason: “A minus B” means “in A and not in B.”

#### Group 4: complements of the same event

\[
\Omega\setminus(B\cap C\setminus A)=[B\cap C\cap A^c]^c
\]

Reason:

\[
B\cap C\setminus A=B\cap C\cap A^c
\]

So both expressions mean the complement of \(B\cap C\cap A^c\).

---

# Part 3 — Probability axioms and basic probability rules

## 3.1 Axioms of probability

For any event \(A\):

\[
0\leq P(A)\leq 1
\]

The sample space is certain:

\[
P(\Omega)=1
\]

If A and B are disjoint:

\[
A\cap B=\varnothing
\]

then:

\[
P(A\cup B)=P(A)+P(B)
\]

---

## 3.2 Results derived from the axioms

### Complement rule

\[
P(A^c)=1-P(A)
\]

### Empty event

\[
P(\varnothing)=0
\]

### Difference rule

\[
P(A\setminus B)=P(A)-P(A\cap B)
\]

### Union rule for two events

\[
P(A\cup B)=P(A)+P(B)-P(A\cap B)
\]

You subtract the overlap because it was counted twice.

### Union rule for three events

\[
P(A\cup B\cup C)=P(A)+P(B)+P(C)-P(A\cap B)-P(A\cap C)-P(B\cap C)+P(A\cap B\cap C)
\]

Pattern: add singles, subtract pairwise overlaps, add triple overlap back.

---

# Part 4 — Equal a priori probabilities

## 4.1 Core idea

If all outcomes are equally likely, then:

\[
P(A)=\frac{\text{number of favourable outcomes}}{\text{number of total outcomes}}
\]

or:

\[
P(A)=\frac{n_A}{n_\Omega}
\]

### Problem-solving method

1. Identify the total equally likely outcomes.
2. Count the outcomes in the event.
3. Divide favourable by total.

### Example
A fair die has sample space:

\[
\Omega=\{1,2,3,4,5,6\}
\]

Let A be “roll an even number.”

\[
A=\{2,4,6\}
\]

So:

\[
P(A)=\frac{3}{6}=\frac12
\]

---

# Part 5 — Independent events, conditional probability, and Bayes’ theorem

## 5.1 Independent events

Events A and B are independent if knowing that one happened does not change the probability of the other.

If A and B are independent:

\[
P(A\cap B)=P(A)P(B)
\]

### Example
Roll two dice.

A = first die is even.

B = second die is 6.

\[
P(A)=\frac12
\]

\[
P(B)=\frac16
\]

Since the dice do not affect each other:

\[
P(A\cap B)=\frac12\cdot \frac16=\frac1{12}
\]

---

## 5.2 Conditional probability

Conditional probability means “probability of B given A.”

\[
P(B|A)=\frac{P(A\cap B)}{P(A)}
\]

Rearranged:

\[
P(A\cap B)=P(A)P(B|A)
\]

Also:

\[
P(A\cap B)=P(B)P(A|B)
\]

### Tutor interpretation

When information is revealed, your sample space shrinks.

Example: if you are told a die roll is odd, the possible outcomes become:

\[
\{1,3,5\}
\]

So the probability of rolling 5 given odd is:

\[
\frac13
\]

not \(\frac16\).

---

## 5.3 Bayes’ theorem

Bayes’ theorem lets you reverse conditional probabilities.

\[
P(A|B)=\frac{P(A)P(B|A)}{P(B)}
\]

If A and \(A^c\) exhaust the sample space:

\[
P(B)=P(A)P(B|A)+P(A^c)P(B|A^c)
\]

So:

\[
P(A|B)=\frac{P(A)P(B|A)}{P(A)P(B|A)+P(A^c)P(B|A^c)}
\]

For multiple mutually exclusive exhaustive cases \(A_i\):

\[
P(A_j|B)=\frac{P(A_j)P(B|A_j)}{\sum_i P(A_i)P(B|A_i)}
\]

### Pattern
Use Bayes when the problem gives:

- probability of evidence given cause, \(P(B|A)\),
- but asks for probability of cause given evidence, \(P(A|B)\).

---

# Part 6 — Question Sheet 1, Questions 3–4: Conditional information problems

## 6.1 Monty Hall problem

### Problem
There are 3 doors. One has a car, two have goats. You choose one door. Monty knows where the car is and opens a different door showing a goat. Should you switch?

### Solution
At the start:

\[
P(\text{your first choice is car})=\frac13
\]

\[
P(\text{car is in the other two doors})=\frac23
\]

Monty deliberately opens a goat door. He is not opening randomly. He uses knowledge.

Therefore, after Monty opens a goat door:

- staying wins with probability \(\frac13\),
- switching wins with probability \(\frac23\).

### Answer
You should switch.

\[
P(\text{win by switching})=\frac23
\]

### Pattern
When someone with information deliberately reveals a non-winning option, the remaining unopened option inherits the probability of the whole group it came from.

---

## 6.2 Parachute problem

### Problem
There are 3 parachutes, 1 dud and 2 working. You and another passenger each choose one. Is there an advantage to being second, waiting to see whether the first parachute opens?

### Solution
Before anything happens, your chance of having a working parachute is:

\[
\frac23
\]

If the other passenger jumps first:

- If their parachute fails, yours must work.
- If their parachute works, yours has probability \(\frac12\) of working.

Overall:

\[
P(\text{survive second})=P(\text{other works})P(\text{you work}|\text{other works})+P(\text{other fails})P(\text{you work}|\text{other fails})
\]

\[
=\frac23\cdot\frac12+\frac13\cdot1
\]

\[
=\frac13+\frac13=\frac23
\]

### Answer
There is no probability advantage to being second.

### Difference from Monty Hall
Monty deliberately reveals a goat because he knows where the car is. The passenger does not deliberately reveal a safe or unsafe parachute. Their result is random.

### Pattern
Conditional information helps only if the information is generated in a biased or knowledge-based way. Random information does not automatically create a Monty-Hall advantage.

---

# Part 7 — Counting principles

## 7.1 Addition principle

If choices are disjoint, add them.

Example: If you have \(m\) apples and \(n\) oranges, and you choose one fruit, there are:

\[
m+n
\]

choices.

Use addition when the problem says “or.”

---

## 7.2 Multiplication principle

If a process has stages, multiply the number of choices at each stage.

If there are \(n_1\) choices for stage 1, \(n_2\) choices for stage 2, ..., \(n_r\) choices for stage r, then total outcomes:

\[
n_1n_2\cdots n_r
\]

Use multiplication when the problem says “and then.”

### Example
A registration number has 3 letters followed by 3 digits, with repetition allowed.

\[
26\times26\times26\times10\times10\times10
\]

If repetition is not allowed:

\[
26\times25\times24\times10\times9\times8
\]

---

# Part 8 — Permutations and combinations

## 8.1 Factorial

\[
n!=n(n-1)(n-2)\cdots 3\cdot2\cdot1
\]

Also:

\[
0!=1
\]

---

## 8.2 Permutations: order matters

If all \(n\) objects are different, the number of ways to arrange them is:

\[
n!
\]

If choosing and ordering \(r\) objects from \(n\):

\[
{}^nP_r=\frac{n!}{(n-r)!}
\]

### Pattern
Use permutations when:

- order matters,
- positions matter,
- arrangement matters,
- first/second/third matters.

---

## 8.3 Distinguishable permutations with repeated objects

If you have \(n\) total objects, where some are repeated:

\[
\frac{n!}{n_1!n_2!\cdots n_m!}
\]

where \(n_1,n_2,\ldots,n_m\) are the numbers of identical objects of each type.

### Example
ELEVEN has 6 letters:

\[
E,E,E,L,V,N
\]

There are 3 repeated E’s.

\[
\frac{6!}{3!}=120
\]

---

## 8.4 Combinations: order does not matter

The number of ways to choose \(r\) objects from \(n\), when order does not matter, is:

\[
\binom nr={}^nC_r=\frac{n!}{r!(n-r)!}
\]

This is read as “n choose r.”

### Pattern
Use combinations when:

- choosing a group,
- order does not matter,
- poker hands,
- committees,
- selecting cards,
- choosing fish from a lake.

---

# Part 9 — Question Sheet 1, Question 5: Binomial coefficient identities

## 9.1 Prove \({}^nC_0=1\)

\[
{}^nC_0=\frac{n!}{0!(n-0)!}
\]

Since \(0!=1\):

\[
{}^nC_0=\frac{n!}{1\cdot n!}=1
\]

### Meaning
There is exactly one way to choose nothing from \(n\) objects.

---

## 9.2 Prove \({}^nC_{n-k}={}^nC_k\)

\[
{}^nC_{n-k}=\frac{n!}{(n-k)![n-(n-k)]!}
\]

Since:

\[
n-(n-k)=k
\]

\[
{}^nC_{n-k}=\frac{n!}{(n-k)!k!}={}^nC_k
\]

### Meaning
Choosing \(n-k\) things to include is equivalent to choosing \(k\) things to exclude.

---

## 9.3 Prove Pascal’s identity

\[
{}^nC_k+{}^nC_{k+1}={} ^{n+1}C_{k+1}
\]

### Combinatorial proof
Suppose you want to choose \(k+1\) people from \(n+1\) people. Pick one special person.

Case 1: the special person is chosen.

Then choose the remaining \(k\) from the other \(n\):

\[
{}^nC_k
\]

Case 2: the special person is not chosen.

Then choose all \(k+1\) from the other \(n\):

\[
{}^nC_{k+1}
\]

Total:

\[
{}^nC_k+{}^nC_{k+1}={} ^{n+1}C_{k+1}
\]

---

# Part 10 — Question Sheet 1, Question 6: Galileo’s dice problem

## 10.1 Problem
Three dice are rolled. The sums 9 and 10 can each be made in six unordered ways. Why is 10 more likely?

## 10.2 Total ordered outcomes
Each die has 6 possibilities:

\[
6^3=216
\]

Each ordered triple is equally likely.

---

## 10.3 Sum 9
Unordered patterns:

\[
(1,2,6),(1,3,5),(1,4,4),(2,2,5),(2,3,4),(3,3,3)
\]

Count ordered permutations:

| Pattern | Ordered arrangements |
|---|---:|
| \((1,2,6)\) | 6 |
| \((1,3,5)\) | 6 |
| \((1,4,4)\) | 3 |
| \((2,2,5)\) | 3 |
| \((2,3,4)\) | 6 |
| \((3,3,3)\) | 1 |

Total:

\[
25
\]

So:

\[
P(9)=\frac{25}{216}
\]

---

## 10.4 Sum 10
Unordered patterns:

\[
(1,3,6),(1,4,5),(2,2,6),(2,3,5),(2,4,4),(3,3,4)
\]

Count ordered permutations:

| Pattern | Ordered arrangements |
|---|---:|
| \((1,3,6)\) | 6 |
| \((1,4,5)\) | 6 |
| \((2,2,6)\) | 3 |
| \((2,3,5)\) | 6 |
| \((2,4,4)\) | 3 |
| \((3,3,4)\) | 3 |

Total:

\[
27
\]

So:

\[
P(10)=\frac{27}{216}=\frac18
\]

### Final answer

\[
P(10)>P(9)
\]

because 10 has more ordered outcomes, even though both 9 and 10 have six unordered patterns.

### Pattern
When dice are rolled, the dice are distinguishable by position: die 1, die 2, die 3. Therefore, ordered outcomes matter.

---

# Part 11 — Question Sheet 1, Question 7: Word permutations

## 11.1 Total permutations of ELEVEN

ELEVEN has letters:

\[
E,E,E,L,V,N
\]

There are 6 letters, with 3 identical E’s.

\[
\frac{6!}{3!}=120
\]

### Answer

\[
120
\]

---

## 11.2 Begin and end with E

Fix E at the beginning and end:

\[
E\_\_\_\_E
\]

Remaining letters:

\[
E,L,V,N
\]

They are all distinct, so:

\[
4!=24
\]

### Answer

\[
24
\]

---

## 11.3 Three E’s together

Treat \(EEE\) as one block.

Objects to arrange:

\[
EEE,L,V,N
\]

There are 4 objects:

\[
4!=24
\]

### Answer

\[
24
\]

### Pattern
If letters must stay together, treat them as one block.

---

# Part 12 — Question Sheet 1, Question 8: Route counting

## 12.1 Problem
There are 5 roads from A to B and 3 roads from B to C.

---

## 12.2 Routes from A to C via B

Choose one A-B road and one B-C road:

\[
5\times3=15
\]

### Answer

\[
15
\]

---

## 12.3 Circular routes A to C and back through B

Outward journey:

\[
5\times3=15
\]

Return journey:

\[
3\times5=15
\]

Total:

\[
15\times15=225
\]

### Answer

\[
225
\]

---

## 12.4 Circular routes using different road sections on return

Outward choices:

\[
5\times3=15
\]

Return from C to B: cannot use the same B-C road, so:

\[
2
\]

Return from B to A: cannot use the same A-B road, so:

\[
4
\]

Total:

\[
15\times2\times4=120
\]

### Answer

\[
120
\]

### Pattern
For multi-stage routes, multiply choices stage by stage. If a road cannot be reused, reduce the available choices.

---

# Part 13 — Question Sheet 1, Question 9: Poker hands

## 13.1 Total number of poker hands

A poker hand is 5 cards chosen from 52. Order does not matter.

\[
\binom{52}{5}=2,598,960
\]

### Answer

\[
2,598,960
\]

---

## 13.2 Hands consisting only of clubs

There are 13 clubs. Choose 5:

\[
\binom{13}{5}=1287
\]

### Answer

\[
1287
\]

---

## 13.3 Flushes

A flush means all 5 cards are the same suit.

Choose the suit:

\[
4
\]

Choose 5 cards from that suit:

\[
\binom{13}{5}
\]

Total:

\[
4\binom{13}{5}=4(1287)=5148
\]

### Answer

\[
5148
\]

---

## 13.4 Exactly two Aces

Choose 2 Aces from 4:

\[
\binom42
\]

Choose remaining 3 cards from the 48 non-Aces:

\[
\binom{48}{3}
\]

Total:

\[
\binom42\binom{48}{3}=103,776
\]

### Answer

\[
103,776
\]

---

## 13.5 At least two Aces

“At least two” means 2, 3, or 4 Aces.

\[
\binom42\binom{48}{3}+\binom43\binom{48}{2}+\binom44\binom{48}{1}
\]

\[
=103,776+4,512+48=108,336
\]

### Answer

\[
108,336
\]

---

## 13.6 Four of a kind

Choose the rank:

\[
13
\]

All 4 suits of that rank are forced.

Choose the fifth card from the remaining 48 cards:

\[
48
\]

Total:

\[
13\times48=624
\]

### Answer

\[
624
\]

---

## 13.7 Full House

A full house has 3 cards of one rank and 2 cards of another rank.

Choose rank for triple:

\[
13
\]

Choose 3 suits from 4:

\[
\binom43
\]

Choose rank for pair:

\[
12
\]

Choose 2 suits from 4:

\[
\binom42
\]

Total:

\[
13\binom43\times12\binom42=3744
\]

### Answer

\[
3744
\]

### Pattern
Poker hands are almost always combination problems because order does not matter.

---

# Part 14 — Question Sheet 1, Question 10: Hypergeometric and repeated capture

## 14.1 Fish without replacement

A lake contains:

- \(b\) bream,
- \(t\) trout,
- total \(b+t\) fish.

You catch \(n\) fish without replacement.

### Problem
Find the probability of catching \(n_b\) bream.

### Solution
Choose \(n_b\) bream from \(b\):

\[
\binom{b}{n_b}
\]

Choose the remaining \(n-n_b\) fish from trout:

\[
\binom{t}{n-n_b}
\]

Choose any \(n\) fish from all \(b+t\):

\[
\binom{b+t}{n}
\]

Therefore:

\[
P(n_b\text{ bream})=\frac{\binom{b}{n_b}\binom{t}{n-n_b}}{\binom{b+t}{n}}
\]

### Pattern
This is a hypergeometric distribution: sampling without replacement from two groups.

---

## 14.2 Fish caught twice after return

### Problem
Catch \(n\) fish, return them alive, then catch \(m\) fish. Find the probability that exactly \(k\) bream are caught twice. Do not assume the first catch had a fixed number of bream.

### Solution strategy
Let \(r\) be the number of bream caught in the first catch. Since \(r\) is unknown, sum over all possible \(r\).

Probability first catch has \(r\) bream:

\[
\frac{\binom br\binom t{n-r}}{\binom{b+t}{n}}
\]

Given that \(r\) bream were caught first, exactly \(k\) of those \(r\) bream must appear again:

\[
\binom rk
\]

The remaining \(m-k\) fish in the second catch must come from the fish that are not those \(r\) first-caught bream. There are \(b+t-r\) such fish:

\[
\binom{b+t-r}{m-k}
\]

Total possible second catches:

\[
\binom{b+t}{m}
\]

Therefore:

\[
P(\text{exactly }k\text{ bream caught twice})
=
\sum_r
\frac{\binom br\binom t{n-r}}{\binom{b+t}{n}}
\cdot
\frac{\binom rk\binom{b+t-r}{m-k}}{\binom{b+t}{m}}
\]

The sum is over all valid \(r\), meaning values for which the combinations make sense.

### Pattern
When an unknown intermediate count exists, condition on it, solve for each possible value, then sum.

---

# Part 15 — Discrete random variables

## 15.1 Random variable

A random variable is a function that assigns a real number to each outcome.

Example: draw 5 cards and let:

\[
X=\text{number of clubs drawn}
\]

The possible values are:

\[
X=0,1,2,3,4,5
\]

---

## 15.2 Probability mass function, PMF

For a discrete random variable \(X\), the probability mass function is:

\[
f(a)=P(X=a)
\]

The probabilities must sum to 1:

\[
\sum_i f(x_i)=1
\]

### Problem pattern
If the problem asks “what is the probability distribution of X?”, list all possible values of X and calculate \(P(X=x)\) for each.

---

## 15.3 Cumulative probability function, CPF

The cumulative probability function is:

\[
F(x)=P(X\leq x)
\]

For discrete X:

\[
F(x)=\sum_{x_i\leq x}f(x_i)
\]

And:

\[
P(a<X\leq b)=F(b)-F(a)
\]

---

## 15.4 Example: number of clubs in a 5-card hand

Let \(X\) be the number of clubs in a 5-card hand.

There are 13 clubs and 39 non-clubs.

Total hands:

\[
\binom{52}{5}
\]

Exactly \(m\) clubs:

\[
\binom{13}{m}\binom{39}{5-m}
\]

So:

\[
P(X=m)=\frac{\binom{13}{m}\binom{39}{5-m}}{\binom{52}{5}}
\]

for \(m=0,1,2,3,4,5\).

### Pattern
This is another hypergeometric distribution: choose successes and failures without replacement.

---

# Part 16 — Expectation, variance, and moments

## 16.1 Expectation value

For a discrete random variable:

\[
E(X)=\sum_i x_i f(x_i)
\]

The expectation is also called:

- mean,
- average,
- first moment,
- \(\mu\),
- \(\langle x\rangle\).

### Interpretation
Expectation is the long-run average value of the random variable.

---

## 16.2 Function of a random variable

If:

\[
Y=g(X)
\]

then:

\[
f_Y(y)=P(g(X)=y)=\sum_{x:g(x)=y}f_X(x)
\]

And:

\[
E[g(X)]=\sum_x g(x)f_X(x)
\]

Special case:

\[
E(aX+b)=aE(X)+b
\]

---

## 16.3 Variance

Variance measures spread around the mean.

\[
V(X)=E[(X-\mu)^2]
\]

where:

\[
\mu=E(X)
\]

Equivalent formula:

\[
V(X)=E(X^2)-[E(X)]^2
\]

Standard deviation:

\[
\sigma=\sqrt{V(X)}
\]

### Useful variance rules

For constants \(a,b\):

\[
V(a)=0
\]

\[
V(aX+b)=a^2V(X)
\]

If \(X\) and \(Y\) are independent:

\[
V(aX+bY)=a^2V(X)+b^2V(Y)
\]

So:

\[
V(X+Y)=V(X)+V(Y)
\]

and:

\[
V(X-Y)=V(X)+V(Y)
\]

provided X and Y are independent.

---

## 16.4 Higher moments

The \(k\)-th moment about zero is:

\[
E(X^k)=\sum_x x^k f(x)
\]

The \(k\)-th central moment is:

\[
E[(X-\mu)^k]=\sum_x (x-\mu)^k f(x)
\]

The variance is the second central moment.

The first central moment is always zero:

\[
E(X-\mu)=0
\]

---

# Part 17 — Probability generating functions

## 17.1 Generating function idea

A generating function stores a whole probability distribution inside one function.

For a discrete random variable \(X\) taking non-negative integer values:

\[
G_X(t)=E(t^X)=\sum_x P(X=x)t^x
\]

The coefficient of \(t^x\) is \(P(X=x)\).

---

## 17.2 Recovering probabilities from PGF

\[
P(X=x)=\frac{G_X^{(x)}(0)}{x!}
\]

where \(G_X^{(x)}(0)
\) is the \(x\)-th derivative evaluated at 0.

---

## 17.3 Moments from PGF

\[
E(X)=G_X'(1)
\]

\[
E[X(X-1)]=G_X''(1)
\]

\[
V(X)=G_X''(1)+G_X'(1)-[G_X'(1)]^2
\]

---

## 17.4 Sum of independent random variables

If \(X\) and \(Y\) are independent:

\[
G_{X+Y}(t)=G_X(t)G_Y(t)
\]

For more variables:

\[
G_{X_1+\cdots+X_n}(t)=G_{X_1}(t)\cdots G_{X_n}(t)
\]

---

# Part 18 — Important discrete distributions

## 18.1 Binomial distribution

### When to use it
Use the binomial distribution when:

1. There are \(n\) repeated trials.
2. Each trial has two outcomes: success or failure.
3. Each trial has the same success probability \(p\).
4. Trials are independent.

### Formula
If:

\[
X\sim \mathrm{Bin}(n,p)
\]

then:

\[
P(X=k)=\binom nk p^k(1-p)^{n-k}
\]

for \(k=0,1,2,\ldots,n\).

### Mean and variance

\[
E(X)=np
\]

\[
V(X)=np(1-p)
\]

### PGF

\[
G_X(t)=(1-p+pt)^n
\]

### Pattern
Use binomial for “number of successes in n independent trials.”

---

## 18.2 Poisson distribution

### When to use it
Use the Poisson distribution when counting rare/random events occurring in a fixed interval of time, space, area, or volume, with average rate \(\lambda\).

Examples:

- emails per hour,
- defects per material sample,
- arrivals per minute,
- radioactive decays in a time interval.

### Formula
If:

\[
X\sim \mathrm{Po}(\lambda)
\]

then:

\[
P(X=k)=\frac{\lambda^k}{k!}e^{-\lambda}
\]

for \(k=0,1,2,\ldots\).

### Mean and variance

\[
E(X)=\lambda
\]

\[
V(X)=\lambda
\]

### PGF

\[
G_X(t)=e^{\lambda(t-1)}
\]

### Sum of independent Poisson variables

If:

\[
X\sim \mathrm{Po}(\lambda_X)
\]

and:

\[
Y\sim \mathrm{Po}(\lambda_Y)
\]

then:

\[
X+Y\sim \mathrm{Po}(\lambda_X+\lambda_Y)
\]

### Pattern
Poisson is often the limit of a binomial distribution when \(n\) is large, \(p\) is small, and \(np=\lambda\) remains moderate.

---

# Part 19 — Continuous random variables

## 19.1 Continuous distribution

A continuous random variable can take values over an interval, such as height, time, or length.

For continuous variables, probabilities are given by areas under a density curve.

---

## 19.2 Probability density function, PDF

For a continuous random variable \(X\), the PDF \(f(x)\) satisfies:

\[
P(x<X<x+\Delta x)\approx f(x)\Delta x
\]

and:

\[
P(a<X<b)=\int_a^b f(x)\,dx
\]

The total area must be 1:

\[
\int_{-\infty}^{\infty}f(x)\,dx=1
\]

For a continuous variable:

\[
P(X=a)=0
\]

because a single point has zero area.

---

## 19.3 Cumulative distribution function, CDF

\[
F(x)=P(X\leq x)
\]

For continuous variables:

\[
F(x)=\int_{-\infty}^x f(u)\,du
\]

And:

\[
P(a<X\leq b)=F(b)-F(a)
\]

PDF from CDF:

\[
f(x)=\frac{dF(x)}{dx}
\]

---

## 19.4 Moments of a continuous distribution

Mean:

\[
E(X)=\int_{-\infty}^{\infty}x f(x)\,dx
\]

Function expectation:

\[
E[g(X)]=\int_{-\infty}^{\infty}g(x)f(x)\,dx
\]

Variance:

\[
V(X)=E[(X-\mu)^2]
\]

or:

\[
V(X)=E(X^2)-[E(X)]^2
\]

---

# Part 20 — Moment generating functions

## 20.1 Definition

For a random variable \(X\), the moment generating function is:

\[
\Psi_X(t)=E(e^{tX})
\]

For discrete X:

\[
\Psi_X(t)=\sum_x e^{tx}f(x)
\]

For continuous X:

\[
\Psi_X(t)=\int_{-\infty}^{\infty}e^{tx}f(x)\,dx
\]

---

## 20.2 Moments from MGF

The \(n\)-th derivative at \(t=0\) gives the \(n\)-th moment:

\[
\Psi_X^{(n)}(0)=E(X^n)
\]

So:

\[
\Psi_X'(0)=E(X)
\]

\[
\Psi_X''(0)=E(X^2)
\]

Then:

\[
V(X)=\Psi_X''(0)-[\Psi_X'(0)]^2
\]

---

## 20.3 MGF of a sum

If X and Y are independent:

\[
\Psi_{X+Y}(t)=\Psi_X(t)\Psi_Y(t)
\]

---

# Part 21 — Important continuous distributions

## 21.1 Gaussian / normal distribution

### Formula

\[
f(x)=\frac{1}{\sigma\sqrt{2\pi}}\exp\left[-\frac{(x-\mu)^2}{2\sigma^2}\right]
\]

Notation:

\[
X\sim N(\mu,\sigma^2)
\]

Mean:

\[
E(X)=\mu
\]

Variance:

\[
V(X)=\sigma^2
\]

Standard deviation:

\[
\sigma
\]

### Standard normal

If:

\[
Z=\frac{X-\mu}{\sigma}
\]

then:

\[
Z\sim N(0,1)
\]

Standard normal CDF:

\[
\Phi(z)=P(Z\leq z)
\]

### Pattern
Use normal distribution for measurement errors, natural variation, and sums/averages of many independent contributions.

---

## 21.2 Central limit theorem

If \(X_1,X_2,\ldots,X_n\) are independent random variables with finite means and variances, then for large \(n\), their sum or average tends toward a normal distribution.

For identically distributed variables with mean \(\mu\) and variance \(\sigma^2\):

\[
\bar X=\frac1n\sum_{i=1}^n X_i
\]

has approximately:

\[
\bar X\sim N\left(\mu,\frac{\sigma^2}{n}\right)
\]

So the standard deviation of the sample mean is:

\[
\frac{\sigma}{\sqrt n}
\]

### Pattern
Averages become more stable as sample size increases.

---

## 21.3 Exponential distribution

### When to use it
Use the exponential distribution for waiting times between random events occurring at constant rate.

### Formula

\[
f(x)=\lambda e^{-\lambda x},\qquad x\geq0
\]

CDF:

\[
F(x)=1-e^{-\lambda x}
\]

Survival probability:

\[
P(X>x)=e^{-\lambda x}
\]

Mean:

\[
E(X)=\frac1\lambda
\]

Variance:

\[
V(X)=\frac1{\lambda^2}
\]

### Memoryless property

\[
P(X>s+t|X>s)=P(X>t)
\]

### Pattern
Use exponential for “time until next event.”

---

## 21.4 Uniform distribution

### Continuous uniform distribution
If X is uniformly distributed on \([a,b]\):

\[
f(x)=\frac1{b-a},\qquad a\leq x\leq b
\]

Mean:

\[
E(X)=\frac{a+b}{2}
\]

Variance:

\[
V(X)=\frac{(b-a)^2}{12}
\]

### Pattern
Use uniform distribution when all values in an interval are equally likely.

---

# Part 22 — Estimation and sample statistics

## 22.1 Population vs sample

A population parameter is a true but usually unknown number, such as:

- true mean \(\mu\),
- true variance \(\sigma^2\),
- true probability \(p\).

A sample statistic is calculated from observed data and used to estimate the parameter.

---

## 22.2 Sample mean

For data:

\[
x_1,x_2,\ldots,x_n
\]

sample mean:

\[
\bar x=\frac1n\sum_{i=1}^n x_i
\]

### Interpretation
\(\bar x\) estimates the population mean \(\mu\).

---

## 22.3 Sample variance

Common unbiased sample variance:

\[
s^2=\frac1{n-1}\sum_{i=1}^n (x_i-\bar x)^2
\]

Sample standard deviation:

\[
s=\sqrt{s^2}
\]

---

## 22.4 Error in the mean

If observations are independent and have standard deviation \(\sigma\), the standard deviation of the mean is:

\[
\frac{\sigma}{\sqrt n}
\]

If \(\sigma\) is unknown, estimate it using \(s\):

\[
\text{standard error of the mean}=\frac{s}{\sqrt n}
\]

### Pattern
Taking more repeated measurements reduces uncertainty in the mean by a factor of \(\sqrt n\), not by \(n\).

---

# Part 23 — Master pattern bank

## 23.1 Set theory patterns

| Problem phrase | Mathematical form |
|---|---|
| A and B | \(A\cap B\) |
| A or B | \(A\cup B\) |
| not A | \(A^c\) or \(\bar A\) |
| A but not B | \(A\setminus B=A\cap B^c\) |
| neither A nor B | \((A\cup B)^c=A^c\cap B^c\) |
| both not A and not B | \(A^c\cap B^c\) |
| everything | \(\Omega\) |
| nothing | \(\varnothing\) |

---

## 23.2 Counting patterns

| Situation | Use | Formula |
|---|---|---|
| sequence of choices | multiplication | \(n_1n_2\cdots n_r\) |
| choose one from disjoint categories | addition | \(m+n\) |
| arrange all distinct objects | permutation | \(n!\) |
| arrange with repeats | repeated permutation | \(\frac{n!}{n_1!n_2!\cdots}\) |
| choose ordered \(r\) from \(n\) | permutation | \(\frac{n!}{(n-r)!}\) |
| choose unordered \(r\) from \(n\) | combination | \(\binom nr\) |
| poker hands | combination | \(\binom{52}{5}\) |
| dice sums | ordered counting | count ordered triples |
| words with repeated letters | repeated permutation | divide by repeated factorials |
| letters together | block method | treat block as one object |

---

## 23.3 Probability model patterns

| Situation | Distribution/model |
|---|---|
| equally likely outcomes | \(P(A)=n_A/n_\Omega\) |
| independent repeated success/failure trials | binomial |
| sampling without replacement from groups | hypergeometric |
| rare/random counts in fixed interval | Poisson |
| waiting time until next event | exponential |
| values equally likely on interval | uniform |
| measurement errors or averages | normal/Gaussian |
| unknown intermediate event | condition then sum |
| evidence updates belief | Bayes’ theorem |

---

# Part 24 — Formula bank

## 24.1 Set identities

\[
A\cap A^c=\varnothing
\]

\[
A\cup A^c=\Omega
\]

\[
\bar\Omega=\varnothing
\]

\[
A\setminus B=A\cap B^c
\]

\[
(A\cup B)^c=A^c\cap B^c
\]

\[
(A\cap B)^c=A^c\cup B^c
\]

---

## 24.2 Probability rules

\[
0\leq P(A)\leq1
\]

\[
P(\Omega)=1
\]

\[
P(\varnothing)=0
\]

\[
P(A^c)=1-P(A)
\]

\[
P(A\setminus B)=P(A)-P(A\cap B)
\]

\[
P(A\cup B)=P(A)+P(B)-P(A\cap B)
\]

\[
P(A\cup B\cup C)=P(A)+P(B)+P(C)-P(A\cap B)-P(A\cap C)-P(B\cap C)+P(A\cap B\cap C)
\]

If disjoint:

\[
P(A\cup B)=P(A)+P(B)
\]

If independent:

\[
P(A\cap B)=P(A)P(B)
\]

Conditional probability:

\[
P(B|A)=\frac{P(A\cap B)}{P(A)}
\]

General multiplication:

\[
P(A\cap B)=P(A)P(B|A)=P(B)P(A|B)
\]

Bayes:

\[
P(A|B)=\frac{P(A)P(B|A)}{P(B)}
\]

Total probability:

\[
P(B)=\sum_i P(B|A_i)P(A_i)
\]

Bayes with multiple cases:

\[
P(A_j|B)=\frac{P(A_j)P(B|A_j)}{\sum_iP(A_i)P(B|A_i)}
\]

---

## 24.3 Counting formulas

Factorial:

\[
n!=n(n-1)(n-2)\cdots2\cdot1
\]

\[
0!=1
\]

Permutations of all distinct objects:

\[
n!
\]

Ordered selection:

\[
{}^nP_r=\frac{n!}{(n-r)!}
\]

Combinations:

\[
\binom nr={}^nC_r=\frac{n!}{r!(n-r)!}
\]

Repeated permutations:

\[
\frac{n!}{n_1!n_2!\cdots n_m!}
\]

Binomial coefficient identities:

\[
{}^nC_0=1
\]

\[
{}^nC_{n-k}={}^nC_k
\]

\[
{}^nC_k+{}^nC_{k+1}={} ^{n+1}C_{k+1}
\]

Binomial expansion:

\[
(a+b)^n=\sum_{k=0}^n \binom nk a^k b^{n-k}
\]

---

## 24.4 Discrete random variable formulas

PMF:

\[
f(x)=P(X=x)
\]

Sum to one:

\[
\sum_x f(x)=1
\]

CPF:

\[
F(x)=P(X\leq x)=\sum_{x_i\leq x}f(x_i)
\]

Interval probability:

\[
P(a<X\leq b)=F(b)-F(a)
\]

Expectation:

\[
E(X)=\sum_x x f(x)
\]

Function expectation:

\[
E[g(X)]=\sum_x g(x)f(x)
\]

Variance:

\[
V(X)=E[(X-\mu)^2]
\]

\[
V(X)=E(X^2)-[E(X)]^2
\]

Standard deviation:

\[
\sigma=\sqrt{V(X)}
\]

Moment:

\[
E(X^k)=\sum_x x^k f(x)
\]

Central moment:

\[
E[(X-\mu)^k]=\sum_x (x-\mu)^k f(x)
\]

---

## 24.5 PGF formulas

\[
G_X(t)=E(t^X)=\sum_x P(X=x)t^x
\]

\[
P(X=x)=\frac{G_X^{(x)}(0)}{x!}
\]

\[
E(X)=G_X'(1)
\]

\[
V(X)=G_X''(1)+G_X'(1)-[G_X'(1)]^2
\]

If independent:

\[
G_{X+Y}(t)=G_X(t)G_Y(t)
\]

---

## 24.6 Discrete distributions

### Binomial

\[
X\sim \mathrm{Bin}(n,p)
\]

\[
P(X=k)=\binom nk p^k(1-p)^{n-k}
\]

\[
E(X)=np
\]

\[
V(X)=np(1-p)
\]

\[
G_X(t)=(1-p+pt)^n
\]

### Poisson

\[
X\sim \mathrm{Po}(\lambda)
\]

\[
P(X=k)=\frac{\lambda^k}{k!}e^{-\lambda}
\]

\[
E(X)=\lambda
\]

\[
V(X)=\lambda
\]

\[
G_X(t)=e^{\lambda(t-1)}
\]

If independent:

\[
X\sim \mathrm{Po}(\lambda_X),\quad Y\sim \mathrm{Po}(\lambda_Y)
\]

then:

\[
X+Y\sim \mathrm{Po}(\lambda_X+\lambda_Y)
\]

### Hypergeometric

\[
P(X=k)=\frac{\binom{K}{k}\binom{N-K}{n-k}}{\binom Nn}
\]

where:

- \(N\) = total population,
- \(K\) = number of successes in population,
- \(n\) = sample size,
- \(k\) = successes drawn.

---

## 24.7 Continuous random variable formulas

PDF normalization:

\[
\int_{-\infty}^{\infty}f(x)dx=1
\]

Probability:

\[
P(a<X<b)=\int_a^b f(x)dx
\]

CDF:

\[
F(x)=P(X\leq x)=\int_{-\infty}^{x}f(u)du
\]

PDF from CDF:

\[
f(x)=F'(x)
\]

Expectation:

\[
E(X)=\int_{-\infty}^{\infty}xf(x)dx
\]

Function expectation:

\[
E[g(X)]=\int_{-\infty}^{\infty}g(x)f(x)dx
\]

Variance:

\[
V(X)=E(X^2)-[E(X)]^2
\]

---

## 24.8 Moment generating function formulas

\[
\Psi_X(t)=E(e^{tX})
\]

Discrete:

\[
\Psi_X(t)=\sum_x e^{tx}f(x)
\]

Continuous:

\[
\Psi_X(t)=\int_{-\infty}^{\infty}e^{tx}f(x)dx
\]

Moments:

\[
\Psi_X^{(n)}(0)=E(X^n)
\]

Mean:

\[
\Psi_X'(0)=E(X)
\]

Second moment:

\[
\Psi_X''(0)=E(X^2)
\]

Variance:

\[
V(X)=\Psi_X''(0)-[\Psi_X'(0)]^2
\]

---

## 24.9 Continuous distributions

### Normal distribution

\[
X\sim N(\mu,\sigma^2)
\]

\[
f(x)=\frac{1}{\sigma\sqrt{2\pi}}\exp\left[-\frac{(x-\mu)^2}{2\sigma^2}\right]
\]

\[
E(X)=\mu
\]

\[
V(X)=\sigma^2
\]

Standardization:

\[
Z=\frac{X-\mu}{\sigma}\sim N(0,1)
\]

### Exponential distribution

\[
f(x)=\lambda e^{-\lambda x},\quad x\geq0
\]

\[
F(x)=1-e^{-\lambda x}
\]

\[
P(X>x)=e^{-\lambda x}
\]

\[
E(X)=\frac1\lambda
\]

\[
V(X)=\frac1{\lambda^2}
\]

### Uniform distribution

\[
X\sim U(a,b)
\]

\[
f(x)=\frac1{b-a},\quad a\leq x\leq b
\]

\[
E(X)=\frac{a+b}{2}
\]

\[
V(X)=\frac{(b-a)^2}{12}
\]

---

## 24.10 Estimation formulas

Sample mean:

\[
\bar x=\frac1n\sum_{i=1}^n x_i
\]

Unbiased sample variance:

\[
s^2=\frac1{n-1}\sum_{i=1}^n(x_i-\bar x)^2
\]

Sample standard deviation:

\[
s=\sqrt{s^2}
\]

Standard error of the mean:

\[
\mathrm{SE}(\bar x)=\frac{s}{\sqrt n}
\]

If the true standard deviation \(\sigma\) is known:

\[
\mathrm{SD}(\bar X)=\frac{\sigma}{\sqrt n}
\]

---

# Part 25 — Final exam strategy checklist

## Before solving, ask these questions

1. Is this a set/Venn diagram question?
   - Translate symbols into plain English.

2. Are all outcomes equally likely?
   - Use favourable / total.

3. Does order matter?
   - Yes: permutation.
   - No: combination.

4. Are there repeated objects?
   - Divide by factorials of repeated groups.

5. Is it sampling without replacement?
   - Use combinations/hypergeometric.

6. Is it repeated success/failure with replacement or independence?
   - Use binomial.

7. Is it a random count in a fixed interval?
   - Use Poisson.

8. Is it a waiting time?
   - Use exponential.

9. Is information revealed?
   - Use conditional probability or Bayes.

10. Is there an unknown intermediate value?
   - Condition on it and sum over all possible values.

---

# Part 26 — Common mistakes to avoid

1. Do not confuse \(A\cup B\) with \(A\cap B\).
   - Union = or.
   - Intersection = and.

2. Do not forget that \(A\setminus B\) means remove B from A.

3. Do not count unordered dice patterns when dice are actually ordered.

4. Do not use permutations for poker hands.
   - Poker hands are combinations.

5. Do not forget to divide by repeated letters in word problems.

6. Do not treat Monty Hall as random opening.
   - Monty knows and deliberately opens a goat.

7. Do not assume the first fish catch has a fixed number of bream in Question 10(b).
   - You must sum over possible first-catch bream counts.

8. Do not confuse PMF and PDF.
   - PMF gives probabilities directly.
   - PDF gives density; probabilities are areas.

9. Do not forget that continuous variables have \(P(X=a)=0\).

10. Do not confuse standard deviation with variance.
    - Variance is \(\sigma^2\).
    - Standard deviation is \(\sigma\).

---

# Part 27 — One-page mini summary

Probability is about assigning numbers to events. An event is a subset of the sample space \(\Omega\). Use set notation to describe events: \(\cap\) means “and,” \(\cup\) means “or,” complement means “not,” and \(\setminus\) means “but not.” If all outcomes are equally likely, probability is favourable outcomes divided by total outcomes.

Counting is the main skill in early probability. Use multiplication for staged choices, permutations when order matters, combinations when order does not matter, and repeated-permutation formulas when objects are identical. Dice rolls are ordered outcomes; poker hands are unordered combinations.

Conditional probability changes the sample space after information is given. Independence means information about one event does not change the probability of another. Bayes’ theorem reverses conditional probabilities.

Discrete random variables have PMFs; continuous random variables have PDFs. Expectation is the weighted average, variance measures spread, and standard deviation is the square root of variance. Generating functions and moment generating functions package distributions into functions that can be differentiated to obtain probabilities or moments.

The core distributions are binomial for independent success/failure trials, hypergeometric for sampling without replacement, Poisson for random counts, exponential for waiting times, uniform for equal density over an interval, and normal/Gaussian for measurement variation and averages.

