---
layout: default
title: "Lecture 1: Introduction, Primitive Java"
---

Why are you here?
=================

Computer programming is an essential skill not only in the field of computing, but also engineering, science, mathematics, and every discipline involving quantitative data. For example: engineers build models of systems before building the systems themselves, in order to understand the important issues. The computer is the ultimate tool for modeling and simulation.

In this course, we will learn about the techniques needed to write complex programs and to understand their behavior.

Review of Primitive Java
========================

"Primitive Java" - the subset of Java that is essentially C.

A Java program is a collection of Java classes. A Java class is a user-defined data type, very much like a C struct type. However, in addition to having fields (member variables), a Java class also has methods (member functions). A class is a way to add "behavior" to instances of a user-defined data type. This is the key idea in *object-oriented programming*, which will be a major theme of this course.

Example Java class (type and run in within Eclipse):

{% highlight java %}
public class Hello {
  public static void main(String[] args) {
    System.out.println("Hello, world!");
  }
}
{% endhighlight %}

Things to note:

-   A class is a sequence of fields and methods. In the **Hello** class, there is a single method, called **main**.
-   The **main** method returns **void**, is **public** and **static**. **public** means it's accessible by other classes. **static** means it is not an *instance method*. When you see **static** on a method, you should think of it as being like a C function.
-   **System.out.println** is a method call which prints text to the console.

Getting information from the keyboard
=====================================

Here's a slightly more interesting Java program:

{% highlight java %}
import java.util.Scanner;

public class Hello {
  public static void main(String[] args) {
    Scanner keyboard = new Scanner(System.in);  // (1)

    System.out.println("What is your name? ");  // (2)
    String name = keyboard.next();              // (3)

    System.out.println("Hello, " + name);       // (4)
  }
}
{% endhighlight %}

The **import** directive tells the Java compiler that we want to use the **java.util.Scanner** class. This class is very useful for reading information, such as text strings, numbers, etc. from the keyboard,

Line 1 of the **main** method creates an *instance* of the **java.util.Scanner** class. In Java, an instance of a class is called an *object*. We'll talk more about this idea next time, but for now, just think of this line as causing a **Scanner** reading from the keyboard to come into existence. We use the variable called **keyboard** to refer to the newly-created **Scanner**.

Line 3 uses the **Scanner** object to read a string value from the keyboard, and saves the string in a variable called **name**. This is an example of calling an *instance method*. Specifically, we're calling the **next** method on the **Scanner** object referred-to by the variable **keyboard**. A method call is a request for an object to do something. We'll talk more about method calls next time. For now, remember that a method call is the most important way to get something done in an object-oriented program.

Line 4 prints some text to the console. It uses *string concatenation* to combine the fixed string value "Hello, " with whatever string the user typed when line 3 was executed. In Java, the plus (+) operator performs string concatenation whenever at least one of its operands is a string.

System.out.printf
=================

The built-in **System.out.printf** method in Java works almost exactly the same way as the **printf** function in C. Here's a variation on the program above:

{% highlight java %}
import java.util.Scanner;

public class Hello {
  public static void main(String[] args) {
    Scanner keyboard = new Scanner(System.in);

    System.out.println("What is your name? ");
    String name = keyboard.next();

    System.out.printf("Hello, %s\n", name);
  }
{% endhighlight %}

Arithmetic
==========

Java supports many familiar numeric data types and operators that are present in C. For example:

> C data type|Java data type
> -----------|--------------
> int|int
> short|short
> char|char
> float|float
> double|double
>
Pretty easy to remember, huh?

Here's a simple program which does a computation on two integer values:

{% highlight java %}
import java.util.Scanner;

public class Hello {
  public static void main(String[] args) {
    Scanner keyboard = new Scanner(System.in);  // (1)

    System.out.println("Enter two integers:");  // (2)
    int a = keyboard.nextInt();                 // (3)
    int b = keyboard.nextInt();                 // (4)

    int sum = a + b;                            // (5)
    System.out.println("The sum is " + sum);    // (6)
  }
}
{% endhighlight %}

Lines 3 and 4 use the **Scanner** class's **nextInt** method to read an integer value.

Line 6 demonstrates that string concatenation works for combining a string value with a numeric value.

Summary
=======

-   Java is *object-oriented*
-   A class is a user-defined data type, like a struct type in C, but you can add *behavior* to it
-   A *method* is a function that belongs to a class and can perform operations on it
-   "Primitive" Java is a subset of Java that is very similar to C
-   Use **System.out.println** and **System.out.printf** to print output
-   *String concatenation* creates a new string of characters by appending a value to an existing string
-   Use a **Scanner** object to get input from the user

