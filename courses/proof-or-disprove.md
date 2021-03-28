# Solving Prove or Disprove Questions

Prove or disprove the following

```
∀x,y, x in D(x) ∪ E(x) and y in F(y) s.t. p(x) ∧ q(x, y)
```

```
Prove or disprove the worst case of a Hash Map lookup is O(n)
```

These questions may look faily intimidating with the mathematical symbols, 
but it's fairly common in CS and Math courses (especially advanced level CS). 
You are given a statement (usually with some conditions) and you are 
asked if you can prove the statement to be **true** (prove) or 
**false** (disprove).

But don't fret, we can solve it in 2 parts and the first part doesn't require
you to know more than just basic Logic with Quantifiers. 

Remember in the world of logic, any mathematical statement can either be
**true** or **false**.

The important part of these **prove or disprove** questions is that marks 
are given to the **content** of your justification, simply saying a statement
is true/false generally doesn't give you any marks.

So the goal is **quickly identify** whether a statement is true or false.
Then you can spend the time focusing on the justification. (we'll focus on the 
first part in this post)

## Intuition (∃x)

It's pretty straight forward to tell whether a predicate logic statement is
true/false (e.g. `1 + 1 = 3 in Z`, `In English, the letter B follows after A`).

Things get slighly trickier when we involve **quantifier(s)**. So let's try a few
examples and then see if we can generalize this approach.

Suppose the statement is `Some students in Canada goes to Langara College`. I am
sure you can quickly determine this is true or false. But what's the thinking process?

For me, this translates to `∃x, inCanada(x) ∧ isStudent(x) | x goes to Langara College`.
It means I have to "find someone who lives in Canada and is a student at the same time"
and that "someone goes to Langara College".

Note that the LHS of `|` describes the condition/domain on `x`, so `x` cannot be
a dog nor be in Portugal.

Well, so to prove a statement with existential qualification (`∃x`) to be **true**,
you'll need to find **one** example of `x` that satisfies the **domain**.

> 🧙: (Observation 1) To prove a statement with `∃x` to be **true**, you need 
> to find **only 1** example of **`x` that's in the domain**

## Intuition (∀x)

Second example, suppose the statement is `Every student in Canada goes to 
Langara College`. I am sure you can quickly determine whether this is true or 
false. But what's the thinking process?

For me, I immediately recall my cousin Bob went to Waterloo. 
1. Bob is in Canada
1. Bob is a student
1. Waterloo isn't Langara
1. (from 1-3) Bob is a student in Canada but didn't go to Langara
1. (from 4) `Every student in Canada goes to Langara College` is **false**

This method is called finding a **Counter Example**. If you have a statement
with **universal quantification**, (i.e. Every, For all), to **disprove** the
statement, a quick option is to find a **counter example**.

> 🤦: Is there a simplier way to know what counter example to find?

Yes! And the hint is from step 4 above. In order show a statement is **false**,
we need to show the **negation** is **true**!

`¬[Every student in Canada goes to Langara College]`
1. `¬[For all x, x in Canada AND x is student | x goes to Langara College]` 
1. `¬[∀x, inCanada(x) ∧ isStudent(x) | x goes to Langara College]`
1. `∃x, inCanada(x) ∧ isStudent(x) | ¬(x goes to Lanagara College)` remember
when we apply the negation, we **do not negate the domain**
1. `∃x, inCanada(x) ∧ isStudent(x) | x does not go to Lanagara College`

Now the last line should be familiar! It's our Observation 1. So to show
this is true, we need to find
- Someone in Canada and is a student
- That said person does not go to Langara College

> 🧙: (Observation 2) To prove a statement with `∀x` to be **false**, you need 
> to only find 1 example of **`x` that's in the domain** and `predicate(x)` 
> is **false**

> 🧙: (Observation 2.1) To prove a statement with `∀x` to be **false**, you can
> **negate the statement** (be careful not to negate the domain). And solve it like
> Observation 1.

With Obersation 1 and 2, now you are equipped with new tools to quickly 
determine whether your should **prove** or **disprove** a statement.

## Strategy (TL;DR)

So here's the overall strategy.

1. Try a few examples in the domain.
   - try simple examples and corner case examples
     - e.g. try 0 for `ℤ`, 0, 1 for `ℕ`, 1 for `modulo`, these are all simple
     numbers and also corner cases in those domains
   - If the statement involves `∀x` and you find examples in the domain that
   doesn't work, then you **disprove** using the example you found.
   - If the statement involves `∃x` and you find examples in the domain that
   works, then you **prove** using the example you found.
2. If 1 didn't work,
   - for `∀x`, this probably means the statement is true, and you'll need
   to construct a proof based on the theorems/axioms in the problem area
   - for `∃x s.t. p(x)`, this means the statement is likely false, and you'll 
   need to construct a proof to show that `∀x s.t. ¬p(x)` based on theorems/axioms
   in the problem area

Let's do an example. 

(I just googled this up)
```
If A, B and C are sets, then A − (B ∩ C) = (A − B) ∩ (A − C).
```

This is a `∀x` question, so let's try a few examples of `A, B, C`.

First sample,
```
A = {1}, B = 0, C = 0

LHS = {1} - 0 = {1}
RHS = ({1} - 0) ∩ ({1} - 0) = {1}
LHS = RHS
```
Ok, this is true, so it doesn't help us, let's try another one.

Second sample, let's try to make `B` and `C` different.
```
A = {1, 2}, B = {1} , C = {2} 

LHS = {1, 2} - ({1} ∩ {2}) = {1, 2} - 0 = {1, 2}
RHS = ({1, 2} - {1}) ∩ ({1, 2} - {2}) = {2} ∩ {1} = 0

LHS != RHS
```
Oh wait! This means we have an example to show the statement is **false**!
So we have arrived at a **counter-example** for `∀x`, and we can **disprove**
the statement!

This is what you have to write

> Because the statement doesn't hold for `A = {1, 2}, B = {1} , C = {2}`,
> the statement `∀A, B, C s.t. A − (B ∩ C) = (A − B) ∩ (A − C)` is **false**

Remember, the strategy applies not only to Math courses. The same strategy 
applies to all **prove or disprove** questions in other courses (CS, 
Statistics, Philosophy, etc).

I hope this gives a better understanding of the structure to tackle 
**prove or disprove** questions quickly.
