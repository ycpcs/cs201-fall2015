---
layout: default
title: "Lecture 11: Generic methods, functors"
---

Implementing Generic Methods
============================

Last time we saw how to define and use generic classes (in particular, **ArrayList&lt;E&gt;**).

We also saw how to *use* generic methods such as **Array.sort**. **Array.sort** is a generic method because it is possible to pass it a reference to an array of any element type **T** that implements the **Comparable&lt;T&gt;** interface. Generic methods are extremely useful because they allow us to define *generic algorithms* --- algorithms that can work with any kind of data.

Today we will discuss how to write a generic method.

Bubble Sort
-----------

*Bubble sort* is an extremely simple sorting algorithm. We will see later in the course that it is not an *efficient* sorting algorithm. However, it is easy to understand and implement.

Here is the pseudo-code of bubble sort:

    bubbleSort(array) {
        for (j = array.length - 1; j >= 0; j--) {
            for (i = 1; i <= j; i++) {
                if (array[i - 1] is greater than array[i]) {
                    swap elements i-1 and i in array
                }
            }
        }
    }

On each iteration of the outer loop, the inner loop sweeps from the element 1 of the array towards the end (stopping at **j**). Each iteration of the inner loop compares the two adjacent values at **i-1** and **i**, swapping them if they are out of order. Each time the inner loop completes, then element **j** contains the correct element value.

The algorithm is called bubble sort because large elements "bubble" towards the end of the array.

To implement this algorithm as a generic method, we need a type parameter to represent the type of the elements. We'll call this parameter **E**. Since the algorithm will need to compare adjacent elements, we will require that **E** is a type which is a subtype of the **Comparable&lt;E&gt;** interface:

{% highlight java %}
public static<E extends Comparable<E>> void bubbleSort(E[] arr) {
    for (int j = arr.length - 1; j >= 0; j--) {
        for (int i = 1; i <= j; i++) {
            if (arr[i-1].compareTo(arr[i]) > 0) {
                E tmp = arr[i-1];
                arr[i-1] = arr[i];
                arr[i] = tmp;
            }
        }
    }
}
{% endhighlight %}

When we want to restrict a type parameter to require it to be a subtype of another type, we use the **extends** keyword. For example, in the **bubbleSort** method, the type parameter is specified as

{% highlight java %}
E extends Comparable<E>
{% endhighlight %}

This causes **Comparable&lt;E&gt;** to be the *upper bound* of **E**. Essentially, we can't call the **bubbleSort** method on an array whose element type is not a type which implements **Comparable&lt;E&gt;**.

If you do not explicitly specify an upper bound on a type parameter, the upper bound is **Object**. An upper bound of **Object** means that there is no restriction on what types may be substituted for the type parameter, other than it must be an object or array type.

Here's a test to make sure the **bubbleSort** method works:

{% highlight java %}
public class SortTest extends TestCase {
    private String[] sArr;
    private Integer[] iArr;

    protected void setUp() throws Exception {
        sArr = new String[]{
                "Carl",
                "Bob",
                "Dingus",
                "Alice",
        };

        iArr = new Integer[] {
                0, 67, 36, 70, 56, 69, 1, 96, 32, 35,
        };
    }

    public void testBubbleSort() throws Exception {
        Sort.bubbleSort(sArr);

        assertEquals("Alice", sArr[0]);
        assertEquals("Bob", sArr[1]);
        assertEquals("Carl", sArr[2]);
        assertEquals("Dingus", sArr[3]);

        Sort.bubbleSort(iArr);

        assertEquals((Integer) 0, iArr[0]);
        assertEquals((Integer) 1, iArr[1]);
        assertEquals((Integer) 32, iArr[2]);
        assertEquals((Integer) 35, iArr[3]);
        assertEquals((Integer) 36, iArr[4]);
        assertEquals((Integer) 56, iArr[5]);
        assertEquals((Integer) 67, iArr[6]);
        assertEquals((Integer) 69, iArr[7]);
        assertEquals((Integer) 70, iArr[8]);
        assertEquals((Integer) 96, iArr[9]);
    }
}
{% endhighlight %}

Type parameters are inferred and checked for generic methods (sometimes!)
-------------------------------------------------------------------------

Note that in the tests for the **bubbleSort** method, we never explicitly specified what type should be specified for the type parameter when we called **bubbleSort**. This is because explicitly specifying the type argument is rarely necessary: Java will *infer* the type argument from the arguments you pass to the generic method.

For example, because the parameter of **bubbleSort** is **E[] arr** (an array of elements of type **E**), when we pass **sArr** to **bubbleSort**, Java infers that **E** must mean **String**.

This automatic inference of type arguments is especially useful when the generic method has multiple parameters. If the method parameters have the same type parameter as part of their type, the type parameter serves as a *constraint* on the types of arguments that may be passed. This (in most cases) will prevent you from accidentally calling a generic methods using inappropriate argument types.

Unfortunately, the inference of type parameters is not checked for array parameters.

Consider a generic array copy function:

{% highlight java %}
public static<E> void copyArray(E[] src, E[] dest) {
    // ... copy all elements from src to dest ...
}
{% endhighlight %}

Because parameters **src** and **dest** are declared to have **E[]** (array of element type **E**) as their types, we should not be able to call the **copyArray** method unless we pass two arrays that have the same element type:

{% highlight java %}
String[] arr1 = ...
String[] arr2 = ...
Integer[] arr3 = ...

copyArray(arr1, arr2); // works: E is String
copyArray(arr1, arr3); // would like a compile error: E cannot be both String and Integer
{% endhighlight %}

However, the above code compiles, and when executed, throws an **ArrayStoreException** for the second call to **copyArray**, because an attempt is made to store an **Integer** value into an array of **String** elements. This shows that type parameter constraints are *not* enforced for array parameters.

Interestingly, this problem does not occur for parameters whose types are classes with a type parameter:

{% highlight java %}
public static<E> void copyArrayList(ArrayList<E> src, ArrayList<E> dest) {
    // ... copy all elements from src to dest ...
}

...

ArrayList<String> arr1 = ...
ArrayList<String> arr2 = ...
ArrayList<Integer> arr3 = ...

copyArrayList(arr1, arr2); // works: E is String
copyArrayList(arr1, arr3); // compile error: E cannot be both String and Integer
{% endhighlight %}

Functors
========

A *functor* is a class whose instances are used like functions.

Functors are very useful when used with generic algorithms, because they allow us to "plug in" various implementations of a function used by an algorithm, without requiring any changes to the way the algorithm is implemented.

A good example of a functor is a *comparator*. A comparator is an object whose purpose is to compare two objects of a particular type to determine whether one is less than, equal to, or greater than the other. In other words, a comparator defines a sort order for a particular type of object.

Comparators perform the same task as a **compareTo** method in classes implementing the **Comparable** interface. However, they are more flexible, because they allow us to implement many different sort orders for the same class.

For example, the built-in implementation of the **compareTo** method in the **String** class is case-sensitive, so the string "YCP" compares as less than "ycp". (This is because upper-case letters have lower character codes than lower-case letters.)

We can define a case-insensitive sort order with a comparator. A comparator class is one which implements the **java.util.Comparator&lt;E&gt;** interface:

{% highlight java %}
public class CaseInsensitiveStringComparator implements Comparator<String> {
    public int compare(String left, String right) {
        left = left.toLowerCase(Locale.US);
        right = right.toLowerCase(Locale.US);
        return left.compareTo(right);
    }
}
{% endhighlight %}

Now, all we need is a sorting method that uses a comparator, rather than the built-in **compareTo** method, to sort array elements. Fortunately, the **java.util.Arrays** class has one:

{% highlight java %}
String[] names = new String[]{
    "cARl",
    "Cthulhu",
    "BoB",
    "DINGus",
    "alICE",
};

Arrays.sort(names, new CaseInsensitiveStringComparator());
for (int i = 0; i < sArr.length; i++) {
    System.out.println(names[i]);
}
{% endhighlight %}

This code snippet prints the strings in the array in alphabetical order, ignoring the case of the letters in the strings.
