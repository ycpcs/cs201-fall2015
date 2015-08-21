---
layout: default
title: "Lab 23: Advanced Recursion"
---

Getting Started
===============

Import [CS201\_Lab23.zip](CS201_Lab23.zip) (**File&rarr;Import...&rarr;General&rarr;Existing Projects into Workspace&rarr;Archive File**). You should see a project called **CS201\_Lab23** in the Package Explorer.

Your Task
=========

Implement the following static methods in the class called **Recursion**:

-   **mergeSortWork**
-   **permute**

Note: this lab is challenging! A good goal would be to get at least one of the methods working. If you get both methods working, you have earned a recursion brown belt.

mergeSortWork
-------------

Merge sort is a simple but highly efficient sorting algorithm. It works by sorting a region of a sequence from a given start index (inclusive) to a given end index (exclusive).

The algorithm works as follows:

1.  if the region has less than 2 elements, do nothing (base case)
2.  otherwise,

    1.  divide the region into halves and recursively sort each half
    2.  merge the two sorted halves of the region into a merged list containing all of the elements in the region, in sorted order
    3.  copy the elements from the merged list back to the region of the list being sorted

A method called **merge** is provided to merge the elements in two sorted halves of a region into a single sorted list.

permute
-------

A *permutation* of a sequence is another sequence containing all of the values in the original sequence, but in which those values might be in a different order.

The **permute** method takes a list and returns a set containing all possible permutations of that list.

**There is a very simple way to implement this method using recursion.** Think about what an appropriate base case for this method might be. Then think about how you might use recursion to work towards this base case.

Hints:

-   Use **new HashSet&lt;List&lt;E&gt;&gt;()** to create a set of lists to return from the method.
-   You will probably need to make **multiple** recursive calls.
-   A recursion on a list will typically make progress by making the list shorter. You can make a list **y** shorter by calling **y.remove(***index***)**, where *index* is the index of the element you want to remove. Make sure you do something with the element you removed.

To simplify your algorithm you will probably want to avoid directly modifying a list. Instead, make a copy and modify the copy. You can make a copy of a list by creating a new **ArrayList** and passing the list you want to copy to the constructor:

Approach
--------

When you implement a method, remove the line of code reading

    throw new UnsupportedOperationException("Not implemented yet");

A JUnit test class called **RecursionTest** contains test cases for each method.

As you think about how to implement each method, consider:

-   What is a base case (or base cases) that can be solved without using recursion?
-   How can you find a subproblem which has the same form as the overall problem?
-   How can you extend the solution to the subproblem to solve the overall problem?

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources/index.html) installed, select the project (**CS201\_Lab23**) in the package explorer and then press the blue up arrow button in the toolbar. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Lab23**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **lab23**. The server URL is

> <https://cs.ycp.edu/marmoset/>
