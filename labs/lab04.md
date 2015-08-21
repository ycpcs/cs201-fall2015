---
layout: default
title: "Lab 4: Text File I/O"
---

Start by downloading [CS201\_Lab04.zip](CS201\_Lab04.zip) and importing it into Eclipse. You should see a project called **CS201\_Lab04**.

You will make changes to the class called **Remember**.

Your task
=========

Write a program that "remembers" the name of the last person to run the program.

Here is an example session showing what should happen the *first* time someone runs the program (user input in **bold**):

<pre>
No one has run this program before!
What is your name? <b>Alice</b>
Ok, Alice, I'm writing your name to a file
</pre>

An example session showing what happens the *second* time someone runs the program (user input in **bold**):

<pre>
The last person to run the program was Alice
What is your name? <b>Bob</b>
Ok, Bob, I'm writing your name to a file
</pre>

The next time someone runs the program, it will print Bob's name as the last person to run the program.

Hints
=====

Store the name of the last person to run the program in a text file.

You can use a **FileReader** and **BufferedReader** to read from the file, and a **FileWriter** to create the file.

You will need to be able to determine whether or not the file containing the name has been created. You can do so as follows. Assume that the variable **fileName** is a String containing the name of the file in which the name should be stored:

    File f = new File(fileName);
    if (f.exists()) {
        // the file exists
    } else {
        // the file has not been created yet
    }

If you want to see the file that your program created, right-click on the name of the project, and choose **Refresh**. You should see your file at the top-level of the project in the Package Explorer.

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources.html) installed, select the project (**CS201\_Lab04**) in the package explorer and then press the blue up arrow button in the toolbar. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Lab04**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **lab4**. The server URL is

> <https://cs.ycp.edu/marmoset/>
