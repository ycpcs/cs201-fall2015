---
layout: default
title: "Lecture 15: Generic Algorithms"
---

# Iterable&lt;E&gt;, for each loop

Each collection class supporting the creation of iterators implements the **Iterable&lt;E&gt;** interface. This interface defines a single method:

{% highlight java %}
public Iterator<E> iterator();
{% endhighlight %}

The *for each* loop is a special kind of loop for traversing the elements of a collection. Example:

{% highlight java %}
ArrayList<String> names = new ArrayList<String>();

// add names

for (String name : names) {
    // name is one of the elements of the names ArrayList
    System.out.println(name);
}
{% endhighlight %}

The loop above is exactly equivalent to the following:

{% highlight java %}
for (Iterator<String> i = names.iterator(); i.hasNext(); ) {
    String name = i.next();

    // name is one of the elements of the names ArrayList
    System.out.println(name);
}
{% endhighlight %}

In other words, using a for each loop on an **Iterable** collection creates an iterator to do the traversal. Any object belonging to a class implementing the **Iterable&lt;E&gt;** interface can be used in a for each loop.

Note that you can also use the for each loop with an ordinary array:

{% highlight java %}
String[] names = new String[]{"Alice", "Bob", "Carl"};
for (String name : names) {
    System.out.println(name);
}
{% endhighlight %}

Generic Algorithms
==================

A generic algorithm is one that can work with many possible data structures and many possible kinds of data.

For example, we have already seen (in [Lecture 11](lecture11.html) how to write a generic **bubbleSort** method to sort the elements of an array with any element type (as long as the element type implements the **Comparable** interface).

Pre-built generic algorithms
----------------------------

The **java.util.Collections** class has implementations of a number of general algorithms.

Some examples:

-   **static&lt;T extends Comparable&lt;T&gt;&gt; void sort(List&lt;T&gt; list)** - sort the elements of a **List**
-   **static&lt;T&gt; void sort(List&lt;T&gt; list, Comparator&lt;T&gt; comp)** - sort the elements of a **List** using a specified **Comparator**
-   **static&lt;T&gt; void reverse(List&lt;T&gt; list)** - reverse the elements of a **List**
-   **static&lt;T extends Comparable&lt;T&gt;&gt; T max(Collection&lt;T&gt; c)** - returns the maximum value in a collection
-   **static&lt;T&gt; T max(Collection&lt;T&gt; c, Comparator&lt;T&gt; comp)** - returns the maximum value in a collection, using the given **Comparator** to compare element values
-   **static&lt;T&gt; shuffle(List&lt;T&gt; list)** - randomly shuffle the elements of the given **List**.

The **java.util.Arrays** class contains a number of implementations of generic algorithms which operate on arrays instead of collection objects.

Implementing Generic Algorithms
===============================

Writing methods that implement generic algorithms is fairly easy. There are a few general principles to keep in mind.

**Make them static**. To make an implementation of a generic algorithm applicable to any kind of data structure, it shouldn't be an instance method of any specific class. So, make it a static method of a class. The class doesn't really serve any purpose other than to provide a home for the static method.

**The algorithm should take one or more Collections, Lists, or Sets as parameter(s).** A generic algorithm typically operates on some collection of values, so taking a reference to a collection object is a general way for the implementation of the algorithm to accept its input. Try to choose the most general interface possible: if you can implement the algorithm for any **Collection** (and not just **Lists** or **Sets**), so much the better. Avoid requiring an instance of any concrete collection class (e.g., **ArrayList**) as a parameter.

**Use functors such as Iterators and Comparators**. If you need to traverse the elements of a collection, use an **Iterator**. If you need to compare element values, use a **Comparator**. If it makes sense, allow the algorithm to take a reference to an instance of a functor object, as we did with **bubbleSort** (by allowing it to use a **Comparator** passed as a parameter.) Functors allow maximum flexibility by allowing details of how the algorithm is to be executed to vary according to which functor implementations are used.
