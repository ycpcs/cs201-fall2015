---
layout: default
title: "Lecture 10: Generic Methods and Classes"
---

Generic Methods and Classes
===========================

It is very useful to be able to write and use methods and classes which are *generic*, meaning that they will work with instances of any type of object.

For example, last time we used the **Arrays.sort** static method, which can sort an array of any kind of object, as long as the objects stored in the array implement the **Comparable** interface (so **Array.sort** can use the **compareTo** method to determine the correct sorted order).

Because it works with any kind of objects, **Arrays.sort** is a generic method.

It is also useful to have generic classes. A generic class is one which can store references to any kind of object. The ability to make a class generic is especially useful for *container classes*, also known as *collections*. A container class is one which stores references to a collection of other objects. Containers are very useful when the program will need to keep track of an arbitrary (and unpredictable) amount of data when it runs.

It is worth mentioning that an array is a kind of container, and potentially even a generic container. The main limitation of arrays as containers is that once an array object is created, its size is fixed, and cannot be expanded dynamically.

Generic Types
=============

To be able to implement generic methods and containers, we need the abililty to define generic *types* in the program. A generic type is one that could point to objects of many different classes.

There are two approaches to generic types in Java: **java.lang.Object**, and *type parameters*.

**java.lang.Object** is a possible generic type, because **Object** is the ultimate supertype of all objects and arrays in Java. Using **Object** as a generic type works, but has some problems, as we will see in a moment.

*Type parameters* are a better approach to generic types. When a method or class has a type parameter, you can think of it as a "placeholder" for some actual type (class or array type). When an instance of a generic class is created, or when a generic method is called, actual types are passed as "arguments".

Object as a generic type
========================

Consider the generic **java.util.ArrayList** class. This class works much like an array, except that it can grow as necessary to accomodate any number of element values.

Using **Object** as a generic type, it would be defined something like the following:

{% highlight java %}
public class ArrayList {
    // fields

    public ArrayList() {
        ...
    }

    public void add(Object elt) {
        // add elt to the end of the collection
    }

    public int size() {
        // return number of objects in the collection
    }

    public Object get(int i) {
        // return element i of the collection
    }

    // other methods...
}
{% endhighlight %}

Here's how we might use this version of **ArrayList** to store strings:

{% highlight java %}
BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));

ArrayList names = new ArrayList();

System.out.println("Type some names:");
while(true) {
    String name = reader.readLine();
    if (name == null) {
        break;
    }
    names.add(name);
}

int count =
    countStringsContaining(names, 'J') +
    countStringsContaining(names, 'j');

System.out.println("You entered "+ count + " names containing J");
{% endhighlight %}

Here is the **countStringsContaining** method:

{% highlight java %}
public int countStringsContaining(ArrayList strings, char ch) {
    int count = 0;

    for (int i = 0; i < strings.size(); i++) {
        String s = (String) strings.get(i); // (!)
        if (s.indexOf(ch) >= 0) {
            count++;
        }
    }

    return count;
}
{% endhighlight %}

Note that because the **get** method returns **Object**, we need a type cast in order to get a **String** reference back out of the collection.

This is the weakness of using **Object** as a generic type: these casts can fail!

For example:

{% highlight java %}
ArrayList deck = new ArrayList();
deck.add(new Card(Suit.DIAMONDS, Rank.QUEEN));
deck.add(new Card(Suit.SPADES, Rank.TWO));

int count = countStringsContaining(deck, 'J'); // (!)
{% endhighlight %}

If we accidentally pass an **ArrayList** containing **Card** references to **countStringsContaining**, then we'll get a **ClassCastException** when that method tries to covert a **Card** reference into a **String** reference.

The real problem here is that the type **Object** does not document what kind of objects are being stored in a collection. If the programmer makes a mistake, a **ClassCastException** occurs when the program runs.

In practice, most collections will store a single kind of object. *Type parameters* document what kind of object a collection will store.

Generics using type parameters
==============================

Here's (almost) what **ArrayList** really looks like. It is defined to use a type parameter to represent the type of element stored in the collection:

{% highlight java %}
public class ArrayList<E> {
    // fields

    public ArrayList() {
        ...
    }

    public void add(E elt) {
        // add elt to the end of the collection
    }

    public int size() {
        // return number of objects in the collection
    }

    public E get(int i) {
        // return element i of the collection
    }

    // other methods...
}
{% endhighlight %}

Note that where previously **Object** was used as the generic type, now the type parameter **E** is used.

We can see the advantage by rewriting the same code example as above:

{% highlight java %}
BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));

ArrayList<String> names = new ArrayList<String>();

System.out.println("Type some names:");
while(true) {
    String name = reader.readLine();
    if (name == null) {
        break;
    }
    names.add(name);
}

int count =
    countStringsContaining(names, 'J') +
    countStringsContaining(names, 'j');

System.out.println("You entered "+ count + " names containing J");

...

public int countStringsContaining(ArrayList<String> strings, char ch) {
    int count = 0;

    for (int i = 0; i < strings.size(); i++) {
        String s = strings.get(i); // No cast is needed!
        if (s.indexOf(ch) >= 0) {
            count++;
        }
    }

    return count;
}
{% endhighlight %}

Now instead of creating and using an **ArrayList**, we're creating and using an **ArrayList&lt;String&gt;**. You can read this as "ArrayList of String" elements.

The way to understand this works is by imagining that, in the case of declaring an **ArrayList** of **String** elements, the type parameter **E** is replaced with **String** everywhere in the text of the **ArrayList** class.

Type parameters are a superior approach to generics because the Java compiler enforces the type parameter. So, for example:

-   You can't add a **Card** to an **ArrayList&lt;String&gt;**
-   You can't pass an **ArrayList&lt;Card&gt;** to a method which takes an **ArrayList&lt;String&gt;**

Because the type argument of a collection is enforced when objects are added to the collection, casts are not necessary when getting a reference back out of the collection.

Type erasure
------------

Behind the scenes, Java type parameters work by *type erasure*. The "real" type of a type parameter is actually **Object**: the compiler inserts type casts in the program where necessary to convert **Object** references to whatever argument type is appropriate.
