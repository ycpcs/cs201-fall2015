---
layout: default
title: "Lecture 12a: Code Comments"
---

These notes are based in part on private communication with [Peter DePasquale](http://www.tcnj.edu/~depasqua/).

Comments
========

Why comment your code?

-   Explain the *intent* of the code
-   Describe the purpose of classes and methods, and how they are meant to be used

Kinds of comments
-----------------

Java has three kinds of comments.

**End-of-line comments**: start with **//**, continue to end of line. Example:

{% highlight java %}
// Temporarily block the editor's onChange handler from
// adding changes to the ChangeList.
mode = Mode.LOADING;
{% endhighlight %}

**Block comments**: start with <b>/\*</b>, end with <b>\*/</b>, and may span multiple lines. These are not used very often. Here is the comment above as a block comment:

**Javadoc comments**: a Javadoc comment describes a class, method, or field. Javadoc comments begin with <b>/\*\*</b> and end with <b>\*/</b>, and (like block comments) may span multiple lines. Each javadoc comment should begin with a description of the class, method, or field.

Javadoc comments can use *tags* to describe features of the class, method, or field. For example, a javadoc method comment can use **@param** tags to describe method parameters and a **@return** tag to describe the method's return value. Example javadoc method comment:

{% highlight java %}
/**
 * Factory method to create an error status message.
 *
 * @param message the message text
 * @return the error status message
 */
public static StatusMessage error(String message) {
        return new StatusMessage(Category.ERROR, message);
}
{% endhighlight %}

Example javadoc class comment:

{% highlight java %}
/**
 * A status message describing the outcome of an operation
 * or other interesting piece of information the user should
 * know about.
 *
 * Use the factory methods goodNews(String),
 * error(String), pending(String), and
 * information(String) to create StatusMessage objects.
 *
 * @author David Hovemeyer
 */
public class StatusMessage {
        // ...fields and methods...
{% endhighlight %}

Here are the most commonly-used tags:

> Tag  | Used with  | What it does
> ---  | ---------  | ------------
> **@param**  | methods  | specifies name of parameters, brief description of parameter; there should be one **@param** tag per parameter
> **@return**  | methods  | describes the return value of a method
> **@author**  | classes  | specifies the name of the author of a class; multiple **@author** tags can be used if there are multiple authors

What Javadoc comments are for
-----------------------------

Javadoc comments can be used to produce *API documentation*. A tool that comes with Java, called **javadoc**, reads the javadoc comments from your code and generates a website where each class and method in your program is documented.

For example, here is the API documentation website for the built-in Java libraries:

> <http://docs.oracle.com/javase/6/docs/api/>

You can generate similar documentation for your own programs.

IDEs such as Eclipse will also show you Javadoc documentation when you hover the mouse over a class or method name. This is very useful as a reminder of how each class and method is intended to be used.

Best Practices
==============

Professionalism
---------------

You should strive to make your comments clear and professional. Don't use vulgar language. Some humor is fine, but keep it tasteful. Here's the thing to remember: other people (e.g., potential future employers) will be reading your code! In fact, making your code available online is a great way to build a portfolio of your work.

Code comments
-------------

In comments explaining code (specific statements), describe the "why" rather than the "what". For example:

How many code comments should be added to a program is a matter of judgment. Here are some guidelines:

1.  Any code whose purpose is not obvious should have a comment. **Always** use comments to describe code that is complex or subtle.
2.  Too many comments or excessively verbose comments can make the code difficult to read. Strive to be concise.
3.  Well-written code without comments is better than poorly-written code with comments. (But well-written code *with* comments is better than either!) Always use meaningful names, consistent indentation, and consistent formatting.

Javadoc comments
----------------

Every class and public method should have a javadoc comment. It is not a bad idea to add javadoc comments to private methods as well.

Javadoc comments for methods should have **@param** tags for every method and, if the method is not **void**, should have a **@return** tag to describe the return value.

Javadoc comments for classes should have an **@author** tag.
