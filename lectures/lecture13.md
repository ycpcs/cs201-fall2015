---
layout: default
title: "Lecture 13: Analysis of Algorithms, Big-O"
---

# Analysis of Algorithms

*Algorithm analysis* refers to examining an algorithm and determining, as a function of the size of its input, how many steps the algorithm will take to complete.

General rules:

1.  a program statement that is not a method call: 1 step

2.  loop executing *n* iterations: *n* \* *m*, where *m* is the cost of a single loop iteration (**NOTE**: *m* may be a function of which loop iteration is being executed)

3.  method call: however many steps the method body will take given the arguments passed to the method

Usually, we are interested in the *worst case*: the absolute upper limit for how many steps the algorithm will take.  Sometimes we may be interested in the *average case*, although what consistitutes the *average* case can be difficult to define and complicated to analyze.  The worst case is usually fairly easy to figure out, and algorithms with good worst case behavior give us confidence that our program will run efficiently no matter what input we give it.

A simple example: a linear search for an array element matching a specified value:

{% highlight java %}
public static<E> int findElement(E[] array, E element) {
    for (int i = 0; i < array.length; i++) {
        if (array[i].equals(element)) {
            return i;
        }
    }
    return -1;
}
{% endhighlight %}

In the worst case (the array doesn't contain the element we're looking for), the loop will execute once for each element of the array.  Each loop iteration executes 1 statement (the if).  So, the worst case running time of this algorithm is

> *N* + 1

where *N* is the length of the array.  (We tacked on an extra step for the return statement at the end.)

A more complicated case: finding out whether or not an array contains duplicate elements:

{% highlight java %}
public static<E> boolean containsDuplicates(E[] array) {
    for (int i = 0; i < array.length; i++) {
        E element = array[i];
        for (int j = i + 1; j < array.length; j++) {
            E other = array[j];
            if (element.equals(other)) {
                return true;
            }
        }
    }
    return false;
}
{% endhighlight %}

This algorithm is harder to analysis because the number of iterations of the inner loop is determined by which iteration of the outer loop is executing.

It is clear that the in the worst case, the outer loop will execute once for each element of the array.  The inner loop executes once for each element of the array past element *i*.  We'll say that the inner loop executes two statements, and that one statement executes before the inner loop (element = array[i]).  So, as a series, the number of steps performed by the nested loops together is something like:

> = (1 + 2(*N*-1)) + (1 + 2(*N*-2)) + ... + (1 + 2(1)) + (1 + 2(0))
>  = *N* + 2(*N* \* (*N*/2))
>  = *N* + *N*<sup>2</sup>

(Recall that the sum of the series 1 + 2 + ... + *N*-2 + *N*-1 is *N*\**N*/2.)

Tacking on an extra step for the final return statement and putting the terms in canonical order, we get a worst case cost of

> *N*<sup>2</sup> + *N* + 1

where *N* is the length of the array.

Big-O
-----

In analyzing an algorithm, we are generally interested in its *growth* as *N* increases, rather than an exact number of steps.  *Big-O* refers to characterizing the growth of the exact cost T(n) of an algorithm in relation to a simpler function f(n).  Specifically, the exact cost T(n) of an algorithm is O(f(n)) iff

> There exists some constant *C* such that *C* \* f(n) \>= T(n) for all sufficiently large values of n

Visually, f(n) is an upper bound for T(n) once we reach some sufficiently large value of n:

> ![](figures/big-O.png)

Finding the big-O bound for an algorithm is really easy, once you know its exact cost:

-   Discard all terms except for the *high order* term
-   Discard all constants

You can find the high order term according to the following inequalities (assume k \> 1, j \> k):

> 1 &lt; log n &lt; n<sup>1/k</sup> &lt; n < n<sup>k</sup> &lt; n<sup>j</sup> &lt; k<sup>n</sup>

So, our algorithm to search an array for a specified element is O(N), and the algorithm to determine whether or not an array has duplicate elements is O(N<sup>2</sup>).  In the second case, we had both *N* and *N*<sup>2</sup> terms, but *N*<sup>2</sup> dominates *N*.

Playing fast and loose
----------------------

One of the nice things about analysis using big-O is that you can *immediately* drop low order terms.  For example, it is perfectly valid to say things like:

> That inner loop is O(N<sup>2</sup>), and it executes in an outer loop that is O(N).  So, the entire algorithm is O(N<sup>3</sup>).

Big-O example problems
======================

First problem
-------------

In the following method, let the problem size *N* be **rowsCols**, which is the number of rows and columns in the square two-dimensional array **matrix**.

{% highlight java %}
public static boolean isUpperTriangular(double[][] matrix, int rowsCols) {
    for (int j = 1; j < rowsCols; j++) {
        for (int i = 0; i < j; i++) {
            if (matrix[j][i] != 0.0) {
                return false;
            }
        }
    }
    return true;
}
{% endhighlight %}

As a function of the problem size *N*, what is the big-O upper bound on the worst-case running time of this method?

Also: would our answer be different if *N* was the number of *elements* in **matrix**?

Second problem
--------------

Assume that, in the following problem, **a** and **b** are both square two-dimensional arrays (same number of rows and columns). Let the problem size *N* be the number of rows and columns.

{% highlight java %}
public static double[][] matrixMult(double[][] a, double[][] b) {
    if (a[0].length != b.length) {
        throw new IllegalArgumentException();
    }

    int resultRows = a.length;
    int resultCols = b[0].length;

    double[][] result = new double[resultRows][resultCols];
    for (int j = 0; j < resultRows; j++) {
        for (int i = 0; i < resultCols; i++) {
            // compute dot product of row j in a and col i in b
            double sum = 0;
            for (int k = 0; k < b.length; k++) {
                sum += a[j][k] * b[k][i];
            }
            result[j][i] = sum;
        }
    }

    return result;
}
{% endhighlight %}

As a function of the problem size *N*, what is the big-O upper bound on the worst-case running time of this method?

Again: would the answer be different if *N* was the number of elements in the two arrays?

Third problem
-------------

Assume that, in the following algorithm, the problem size *N* is the number of elements in the array.

{% highlight java %}
// Return the index of the element of the array which is equal to
// searchVal.  Returns -1 if the array does not contain
// any element equal to searchVal.
// Important: the array must be in sorted order for
// this algorithm to work.
public static<E extends Comparable<E>>
int binarySearch(E[] arr, E searchVal) {
    int min = 0, max = arr.length;

    while (min < max) {
        int mid = min + (max-min)/2;

        int cmp = arr[mid].compareTo(searchVal);

        if (cmp == 0) {
            return mid;
        } else if (cmp < 0) {
            max = mid;
        } else {
            min = mid + 1;
        }
    }

    return -1;
}
{% endhighlight %}

As a function of the problem size *N*, what is the big-O upper bound on the worst-case running time of this method?
