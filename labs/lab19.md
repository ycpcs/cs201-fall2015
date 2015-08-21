---
layout: default
title: "Lab 19: Word Count"
---

Getting started
===============

Import [CS201\_Lab19.zip](CS201_Lab19.zip) (**File&rarr;Import...&rarr;General&rarr;Existing Projects into Workspace&rarr;Archive File**). You should see a project called **CS201\_Lab19** in the Package Explorer.

Your Task
=========

Complete the program so that it counts the number of occurrences of words in the text file whose name is entered by the user, and then prints out a histogram showing the number of occurrences of each word (in lower case), listing the words alphabetically.

Code is provided which

-   opens the file
-   reads each line of the file
-   extracts each word (sequence of letters) from the lines of the file, converting each word to lower case

An example text file, **gettysburg.txt**, is provided for you to use when testing your program.

Here is partial output from running the program on this file (user input in **bold**):

<pre>
Read which file? <b>gettysburg.txt</b>
Word counts:
a          : =======
above      : =
add        : =
advanced   : =
ago        : =
all        : =
altogether : =
and        : ======
any        : =
are        : ===
as         : =
battle     : =
</pre>

The length of the "bar" following each word indicates the number of occurrences of that word. For example, the word "and" occurred 6 times, so there are six "=" characters making up the bar for that word.

There are 126 more lines of output.

Hints
=====

Use a map with key type **String** and value type **Integer** to count the number of occurrences of each word.

You are required to list the words alphabetically when displaying the histogram. Can you choose a built-in implementation of the **Map** interface that will make this job easier?

You should determine the length of the longest word so that the "bars" of the histogram will all start in the same column when printed.

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources/index.html) installed, select the project (**CS201\_Lab19**) in the package explorer and then press the blue up arrow button in the toolbar. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Lab19**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **lab19**. The server URL is

> <https://cs.ycp.edu/marmoset/>
