---
layout: default
title: "Lab 11: Functors"
---

Start by downloading [CS201\_Lab11.zip](CS201_Lab11.zip) and importing it into Eclipse. You should see a project called **CS201\_Lab11**.

A Generic Functor interface
===========================

The **Functor** interface defines a very simple kind of functor: one that takes a single argument value, performs some computation on it, and stores the result of the computation in a field or fields:

{% highlight java %}
public interface Functor<E> {
    /**
     * Apply the functor to a value.
     * 
     * @param value a value
     */
    public void apply(E value);
}
{% endhighlight %}

The **ApplyFunctor** class contains a single generic method which is useful for working with **Functor** instances:

{% highlight java %}
public static<E> void applyToArray(E[] arr, Functor<E> functor) {
    for (int i = 0; i < arr.length; i++) {
        functor.apply(arr[i]);
    }
}
{% endhighlight %}

The **applyToArray** method takes an array of elements of type **E** and a **Functor&lt;E&gt;**, and calls the functor's **apply** method on each element of the array. This function may be used to perform a computation on all of the elements in an array.

Your Task
=========

Your task is to implement two classes which implement the **Functor** interface:

1.  **SumIntFunctor**, which implements **Functor&lt;Integer&gt;**. It computes the sum of all of the **Integer** values to which it is applied.
2.  **CountJFunctor**, which implements **Functor&lt;String&gt;**. It computers the number of occurrences of the characters 'J' and 'j' in the **String** values to which it is applied.

The **SumIntFunctorTest** and **CountJFunctorTest** classes implement JUnit tests for both classes.

Hints
=====

The **SumIntFunctor** and **CountJFunctor** classes should build up the overall result by updating the value of a field or fields.

Submitting
==========

When you are done, save the project (**CS201\_Lab11**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **lab11**. The server URL is

> <https://cs.ycp.edu/marmoset/>
