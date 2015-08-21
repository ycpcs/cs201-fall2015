---
layout: default
title: "Lab 22: Binomial Coefficient"
---

Binomial Coefficient
====================

The binomial cooefficient C(n,k), often written "n choose k", is the number of ways to pick a subset of k elements from a collection of n elements. It may be defined recursively as follows:

> C(n,0) = 1
>
> C(n,n) = 1
>
> C(n,k) = C(n-1,k) + C(n-1, k-1)

Getting Started
===============

Import the file [CS201\_Lab22.zip](CS201_Lab22.zip) into your Eclipse workspace. You will implement the **compute** method of the classes **NaiveRecursive** and **Memoization**.

As the names suggest, **NaiveRecursive** should be a literal recursive implementation of the binomial coefficient function, and **Memoization** should implement the binomial coefficient function using memoization to avoid repeatedly solving identical subproblems.

Because the binomial coefficient function takes two parameters, **n** and **k**, you will probably want your memoization table to be a two-dimensional array.

Testing
=======

Run the **main** method of the **TestDriver** class by right-clicking on **TestDriver.java** and choosing **Run As&rarr;Java Application**. The test driver solves C(n,k) for all values of k 0..n, for n=25, and measures the number of milliseconds needed to solve each problem. While the naive recursive implementation will take an appreciable amount of time, the implementation using memoization should execute very quickly.

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources.html) installed, select the project (**CS201\_Lab22**) in the package explorer and then press the blue up arrow button in the toolbar. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Lab22**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **lab22**. The server URL is

> <https://cs.ycp.edu/marmoset/>
