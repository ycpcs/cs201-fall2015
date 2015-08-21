---
layout: default
title: "Lab 13: Big-O"
---

# Your task

Find big-O upper bounds for the following code snippets.  In each, assume that `CODE` is something that completes in constant time (O(1)), and *N* is an integer value representing the problem size.  State your bound in terms of *N*.

Write your answers in a text file (e.g., a file created with Notepad++).  For each answer, explain your reasoning.

As soon as you are done with your answer for the first problem, show your answer to the instructor or a tutor to get some feedback on your approach.

Before you submit, show your work to the instructor or a tutor.

You can check your answers against the [solutions](lab13soln.pdf).

## Problem 1

{% highlight java %}
for (int i = 0; i < N*N; i++) {
    CODE
}
{% endhighlight %}

## Problem 2

{% highlight java %}
for (int i = 0; i < N; i++) {
    CODE
}
for (int i = 0; i < N; i++) {
    CODE
}
{% endhighlight %}

## Problem 3

{% highlight java %}
for (int i = 0; i < N; i++) {
    for (int j = 0; j < i; j++) {
        CODE
    }
}
{% endhighlight %}

Note that the inner loop is dependent on the outer loop, so the inner loop executes a different number of iterations each time it is reached.  In your explanation, you should either:

* Determine how many times `CODE` executes overall (analyzing both loops together): a series sum will be helpful
* State how many times *on average* the inner loop executes when it is reached.

## Problem 4

{% highlight java %}
for (int i = 0; i < 10000000; i++) {
    CODE
}
{% endhighlight %}

## Problem 5

{% highlight java %}
for (int i = 0; i < N; i++) {
    for (int j = 0; j < i*i; j++) {
        CODE
    }
}
{% endhighlight %}

This one is similar to Problem 3: the inner loop is dependent on the outer loop.

## Problem 6

{% highlight java %}
for (int i = 1; i < N; i = i * 2) {
    CODE
}
{% endhighlight %}

Note that **i** is doubling on each loop iteration: how does that affect the number of times the loop will execute?

## Problem 7

{% highlight java %}
for (int i = 0; i < N; i++) {
    for (int j = 0; j < N; j++) {
        for (int k = 0; k < N; k++) {
            CODE
        }
    }
}
{% endhighlight %}

Submitting
==========

Upload the text file containing your answers to the Marmoset server as **lab13**. The server URL is

> <https://cs.ycp.edu/marmoset/>
