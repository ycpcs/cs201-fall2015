---
layout: default
title: "Lab 25: Singly-linked lists"
---

Getting Started
===============

Import [CS201\_Lab25.zip](CS201_Lab25.zip) (**File&rarr;Import...&rarr;General&rarr;Existing Projects into Workspace&rarr;Archive File**). You should see a project called **CS201\_Lab23** in the Package Explorer.

Your Task
=========

The starting code contains a partially-complete implementation of a **LinkedList** class. Your task is to complete the **size**, **add**, **get**, **set**, and **remove** methods. The behavior of these methods should be the usual behavior for list classes:

-   **size** returns the number of elements in the list
-   **add** adds an element to the end of the list
-   **get** gets the element value at a particular index
-   **set** sets (modifies) the element value at a particular index
-   **remove** removes the element value at a particular index

A JUnit test class, **LinkedListTest**, is provided.

Note that when you are done, the **testIteratorRemove** test will still fail. Implementing removal of an element of a linked list using an iterator is challenging. You can try implementing this method (the **remove** method of the **LinkedListIterator** class) if you have time.

Hints
=====

The **remove** method should remove the node containing the selected element from the list.

For each method, sketch out an algorithm on paper before implementing it. Drawing diagrams, especially in the case where the list structure is being modified, is extremely helpful.

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources/index.html) installed, select the project (**CS201\_Lab23**) in the package explorer and then press the blue up arrow button in the toolbar. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Lab25**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **lab25**. The server URL is

> <https://cs.ycp.edu/marmoset/>
