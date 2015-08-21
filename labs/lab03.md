---
layout: default
title: "Lab 3: Arrays"
---

Start by downloading [CS201\_Lab03.zip](CS201_Lab03.zip) and importing it into Eclipse. You should see a project called **CS201\_Lab03**.

Your task
=========

Implement the following static methods in the **Arrays** class:

-   **readArray**: Takes two parameters, **keyboard** and **numElements**. **keyboard** is a **Scanner** object you can use to read input from the user. **numElements** is the number of integer values to read. The method should return a reference to an array containing the requested number of integer values.

-   **printArray**: Takes a parameter **arr**, an array of integer values. The method should print out the element values in the array.

-   **reverseArray**: Takes a parameter **arr**, an array of integer values. The method should reverse the values in the elements of the array. For example, if passed an array containing the values **1 2 3**, the method should re-arrange the contents of the array so that it contains the values **3 2 1**.

Testing
=======

A **main** method is provided for testing - you won't need to change it.

When you run the **main** method, you should see output looking something like this (user input in **bold**):

<pre>
How many values? 
<b>5</b>
Please enter 5 values:
<b>9 0 1 2 5</b>
You entered the following values:
9 0 1 2 5 
Now I am going to reverse the array for you...
Here are the reversed array values:
5 2 1 0 9 
</pre>

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources.html) installed, then right click on the project (**CS201\_Lab03**) and choose **Submit project...**. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Lab03**) to a zip file by right-clicking it and choosing

> **Export...-\>Archive File**

Upload the saved zip file to the Marmoset server as **lab3**. The server URL is

> <https://cs.ycp.edu/marmoset/>
