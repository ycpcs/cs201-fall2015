---
layout: default
title: "Lab 15: Generic Algorithms"
---

Getting Started
===============

Download [CS201\_Lab15.zip](CS201_Lab15.zip). Import it into Eclipse (**File&rarr;Import...&rarr;Existing Projects into Workspace&rarr;Archive File**.) You should see a project called **CS201\_Lab15** in the package explorer.

Your Task
=========

Your task is to implement the five static methods defined in the **Algorithms** class.  *Note*: implement these yourself using an explicit traversal of the input collection, i.e., don't just call a method in **java.util.Collections**.

Hint for the **findMin** and **findMax** methods: you may assume that the collection will have at least one element.

**static&lt;E extends Comparable&lt;E&gt;&gt; E findMin(Collection&lt;E&gt; c)**  
This method should return the minimum (smallest) value in the given **Collection**. Since each element belongs to a class implementing the **Comparable&lt;E&gt;** interface, you can use the **compareTo** method to compare element values.

**static&lt;E extends Comparable&lt;E&gt;&gt; E findMax(Collection&lt;E&gt; c)**  
Like **findMin** above, but return the maximum element value instead of the minimum.

**static&lt;E&gt; E findMin(Collection&lt;E&gt; c, Comparator&lt;E&gt; comp)**  
Like the version of **findMin** that just takes a **Collection**, but uses the **Comparator** parameter to do the element comparisons.

**static&lt;E&gt; E findMax(Collection&lt;E&gt; c, Comparator&lt;E&gt; comp)**  
Like **findMin** above, but return the maximum element value instead of the minimum.

**static&lt;E&gt; int sequentialSearch(List&lt;E&gt; list, E searchVal)**  
Do a sequential search of the given **List**. Return the index of the first occurrence of an element comparing as equal to **searchVal**, or -1 if **searchVal** does not occur in the list. Use the **equals** method to do the comparisons.

A JUnit test class, **AlgorithmsTest**, is provided.

Super-duper extra challenge
===========================

*Optional*: if you finish the above tasks, and your brain isn't completely twisted in knots, rewrite the four **findMin** and **findMax** methods so that three of them are implemented by making a call to the fourth.

**Hint**: Leave your **static&lt;E&gt; E findMin(Collection&lt;E&gt; c, Comparator&lt;E&gt; comp)** as it is. Change the other methods to call it.

**Another hint**: Defining one or more new **Comparator** classes will help.

Let me know if you figure this one out. I may award a prize.

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources/index.html) installed, select the project (**CS201\_Lab15**) in the package explorer and then press the blue up arrow button in the toolbar. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Lab15**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **lab15**. The server URL is

> <https://cs.ycp.edu/marmoset/>
