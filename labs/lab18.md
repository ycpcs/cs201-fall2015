---
layout: default
title: "Lab 18: Palindromes"
---

Getting started
===============

Import [CS201\_Lab18.zip](CS201_Lab18.zip) (**File&rarr;Import...&rarr;General&rarr;Existing Projects into Workspace&rarr;Archive File**). You should see a project called **CS201\_Lab18** in the Package Explorer.

Your Task
=========

A phrase is a palindrome when the sequence of the letters in the phrase is the same both forwards an backwards, ignoring space and punctuation. Some examples:

> Rise to vote, sir
>
> Able was I ere I saw Elba
>
> A man, a plan, a canal - Panama!
>
> A man, a plan, a cat, a ham, a yak, a yam, a hat, a canal - Panama?
>
> A Danish custard? Drat such sin, Ada!

Your task is to write a program which uses a stack to determine whether or not a phrase is a palindrome. A starting point is provided in the **CheckPalindrome** class, whose **main** method reads lines of input from **System.in**. You should modify the loop so that after each line of input is read, it checks the line to see if it is a palindrome, and then prints either "Palindrome" or "Not a palindrome" to **System.out**.

Use two collections: a stack of **Character** values and a queue of **Character** values:

{% highlight java %}
Stack<Character> stack = new Stack<Character>();
Queue<Character> queue = new LinkedList<Character>();
{% endhighlight %}

Note that the **Character** type is essentially equivalent to **char**, but because it is a class, **Character** values can be stored in collections such as **Stack**s. The Java compiler will automatically convert between **char** and **Character** values.

You will need to think about how the stack and queue can help you determine whether or not the input is a palindrome.

Here is an example run (user input in **bold**):

<pre>
<b>A man, a plan, a cat, a ham, a yak, a yam, a hat, a canal - Panama?</b>
Palindrome
<b>Rise to vote, sir</b>
Palindrome
<b>Boy howdy!</b>
Not a palindrome
<b>quit</b>
<i>program exits</i>
</pre>

Requirements and hints
======================

You will need to treat a String object as a sequence of characters. You can use the **length** and **charAt** methods to get the length of a string and the value of a single character of the string, respectively. For example, here is how to iterate over all of the characters in a **String**:

{% highlight java %}
String line = ...
for (int i = 0; i < line.length(); i++) {
    char c = line.charAt(i);

    // Do something with c
}
{% endhighlight %}

Your program should ignore all characters other than letters. You can find out whether or not a character is a letter using the **Character.isLetter** method:

{% highlight java %}
char c = ...

if (Character.isLetter(c)) {
    // c is a letter
}
{% endhighlight %}

You should also ignore case. One way to do this is by converting all letters to lower-case:

{% highlight java %}
c = Character.toLowerCase(c);
{% endhighlight %}

Running the program
===================

Run the **CheckPalindrome** class as a Java Application (right-click, **Run As&rarr;Java Application**).

Type in some phrases and make sure that the program can successfully distinguish palindromes from non-palindromes.

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources/index.html) installed, select the project (**CS201\_Lab18**) in the package explorer and then press the blue up arrow button in the toolbar. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Lab18**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **lab18**. The server URL is

> <https://cs.ycp.edu/marmoset/>
