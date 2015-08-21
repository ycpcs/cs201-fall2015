---
layout: default
title: "Lab 2: Coins class"
---

For this lab you will implement a class that represents a pocketful of change.

Getting Started
===============

Download [CS201\_Lab02.zip](CS201_Lab02.zip). (Save it somewhere you can easily find it again: for example, on the Desktop.)

Start Eclipse. Choose **File&rarr;Import...&rarr;General&rarr;Existing Projects Into Workspace**. Choose **Select archive file**. Choose **CS201\_Lab02.zip** from wherever you saved it earlier. Choose **Finish**.

You should now see the **CS201\_Lab02** project in the Package Explorer window.

Implementing the Coins class
============================

Implement the class called **Coins**, which is in the file called **Coins.java**. This file can be found by expanding the **CS201\_Lab02** project, then the **src** folder, and then the **edu.ycp.cs201.coins** package. Double click on the file to open it in an editor window.

The class should have fields (member variables) for each coin type listed below:

> pennies, nickels, dimes, and quarters

The class should provide the following methods:

1.  A zero-parameter constructor that initializes the new object so that there are 0 pennies, 0 nickels, 0 dimes, and 0 quarters.

2.  A 4-parameter constructor that takes the numbers of pennies, nickels, dimes, and quarters (in that order), and initializes the respective fields.

3.  **findCentsValue** calculates and returns the total value of the coins in cents, as an integer.

4.  **findDollars** calculates and returns the value in dollars, as an integer. Any fractional part of a dollar should be discarded: for example, if the coins total $1.37, then this method should return the value 1.

5.  **findChange** calculates and returns the value of the leftover change (after the dollars are removed) as an integer. For example, if the coins total $1.37, then this method should return the value 37.

Testing
=======

Right-click on **CoinsTest.java** in the package explorer, and choose **Run As...&rarr;JUnit Test**. This will run the JUnit tests for the **Coins** class. If you have correctly implemented the **Coins** class, you will see a green bar, indicating that all tests have succeeded.

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources.html) installed, then right click on the project (**CS201\_Lab02**) and choose **Submit project...**. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Lab02**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **lab2**. The server URL is

> <https://cs.ycp.edu/marmoset/>
