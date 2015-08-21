---
layout: default
title: "Lecture 21: Proof by Induction"
---

Induction Hypothesis
====================

Proof by induction is a very useful technique for proving that a hypothesis is true for **all** integers starting from some small integer (generally 0 or 1). The hypothesis is called the *induction hypothesis*, which we will abbreviate as *IH*. We will say *IH*(0) to refer to the induction hypothesis for the integer 0, *IH*(1) for the integer 1, and *IH*(*n*) for the integer n.

In principle, we could prove the cases of the induction hypothesis one at a time. In other words, prove that *IH*(0) is true, then prove that *IH*(1) is true, then *IH*(2), etc. However, since our goal is to prove the induction hypothesis for **all** integers (greater than our starting point), we will never finish, since there are an infinite number of such integers!

Proof By Induction
==================

Instead, we split up the proof into two steps.

**The Basis Step**. In this step we prove that the induction hypothesis is true for the first integer. For example, if we're starting from 0, then we prove that *IH*(0) is true.

**The Induction Step**. In this step we prove that if *IH*(*n*) is true, then *IH*(*n*+1) must be true.

It should be easy to see how these two steps can be used to "cover" all integers starting from the initial integer up to any arbitrary integer *n*. The basis step proves that the induction hypothesis is true for the first integer. Then, by applying the induction step some finite number of times, we can eventually prove *IH*(*n*) is true for any integer *n*. For example, proving the basis step and the induction step allows us to show that *IH*(3) is true:

> *IH*(0) is true (by the Basis Step)
>
> *IH*(0) implies *IH*(1) (by the Induction Step)
>
> *IH*(1) implies *IH*(2) (by the Induction Step)
>
> *IH*(2) implies *IH*(3) (by the Induction Step)

We can construct such a proof for any *n*, so that means that the induction hypothesis must be true for **all** values of *n*.

Proving the Induction Step
--------------------------

Proving the induction step is typically the more interesting of the two steps. Here is the general approach.

**(1)** State *IH*(*n*) and *IH*(*n*+1). The statement of *IH*(*n*+1) is called the *expectation*, and is extremely important.

**(2)** Show why if *IH*(*n*) is true, then *IH*(*n*+1) must also be true. A very common approach is to define a *recurrence* which, *based on the nature of the property you are trying to prove*, shows how what is true for *n*+1 is related to what is true for *n*. Because the recurrence establishes a link from *n* to *n*+1, it can be used to prove the induction step.

An Example
----------

A concrete example will show how this works. We will prove that the sum of the integers from 1 to *n*, which we will refer to as f(n), is (n(n+1)) / 2. So, the general form of our induction hypothesis is

> f(n) = (n(n+1)) / 2

**Basis Step**. *IH*(1) is f(1) = 1. Since the series of integers from 1 to 1 is simply 1, this is true trivially.

**Induction Step**. First, we will state *IH*(*n*) and *IH*(*n*+1):

> *IH*(*n*) is f(n) = (n(n+1)) / 2
>
> *IH*(*n*+1) is f(n+1) = ((n+1)(n+2))/2

Our statement of *IH*(*n* +1) is the *expectation*. The expectation tells us what we expect to be true if the induction hypothesis is true for *n*+1. We obtained the expectation by simply substuting *n*+1 for *n* in the equation we are trying to prove correct.

Now the critical part: we need to show how what is true for *n*+1 is related to what is true for *n*. Because f(n) is the sum of the integers 1..n, then adding (n+1) to this sum will obviously result in the sum of the integers 1..n+1. We can state this observation as a *recurrence*:

> f(n+1) = f(n) + (n+1)

The recurrence simply states that the sum of the integers 1..n+1 is equal to the sum of the integers 1..n + (n+1).

Now that we have established the recurrence, we can prove the induction step. In the induction step, we show that if or is true, then *IH*(*n*+1) must be true. (Note that we are *not* proving that either *IH*(*n*) or *IH*(*n*+1) is true outright. We are simply proving that if we *assume* that *IH*(*n*) true, then *IH*(*n*+1) must also be true.)

Once we have the recurrence, it is very simple to provie the induction step: we simply expand the occurrence of f(n). We are allowed to assume that *IH*(*n*) is true:

> *IH*(*n*) is f(n) = (n(n+1)) / 2

So, the expanded recurrence is

> f(n+1) = (n(n+1))/2 + (n+1)

Now all we need to do is rearrange the right hand side of the equation so that it matches the *expectation* (which is what we expect if *IH*(*n*+1) is true):

> f(n+1) = (n(n+1))/2 + 2(n+1)/2 &nbsp;&nbsp;&nbsp;&nbsp; *multiply (n+1) by 2/2*
>
> f(n+1) = (n^2+n)/2 + (2n+2)/2 &nbsp;&nbsp;&nbsp;&nbsp; *expand terms*
>
> f(n+1) = (n^2+3n+2)/2 &nbsp;&nbsp;&nbsp;&nbsp; *combine terms*
>
> f(n+1) = ((n+1)(n+2))/2 &nbsp;&nbsp;&nbsp;&nbsp; *factor polynomial*

The expanded recurrence now exactly matches the expectation, proving that if *IH*(*n*) is true, then *IH*(*n*+1) must also be true.

Ta-da!
