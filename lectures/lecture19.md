---
layout: default
title: "Lecture 19: Sets and Maps"
---

Sets
====

A set is a collection which represents a mathematical set. There are two important properties of a set:

-   The same element value may only occur once in a set
-   The order in which the elements of a set appear (when iterating through the elements) is typically different than the order in which the elements were added

The **Set&lt;E&gt;** interface, which is a subclass of **Collection&lt;E&gt;**, describes the important operations. Here are are the three most important set operations:

{% highlight java %}
boolean add(E elt);         // add an element to the set
boolean contains(Object o); // does the set contain given object?
boolean remove(Object o);   // remove given object from the set
{% endhighlight %}

Concrete set implementations typically provide efficient (O(1) or O(log N)) implementations of these methods.

There are two important implementations of the **Set&lt;E&gt;** interface: **HashSet&lt;E&gt;** and **TreeSet&lt;E&gt;**.

**HashSet&lt;E&gt;** implements the set operations in O(N) worst case, O(1) average case. The element type **E** must provide working implementations of the **boolean equals(Object)** and **int hashCode()** methods inherited from **java.lang.Object**. When iterating, the order of the elements of a hash set is arbitrary, and seemingly random.

**TreeSet&lt;E&gt;** implements the set operations in O(log N) worst case and average case. The element type **E** must either implement the **Comparable&lt;E&gt;** interface, or an explicit comparator object (implementing **Comparator&lt;E&gt;**) must be passed to the **TreeSet** constructor when the tree set object is created. When iterating, the elements of a tree set appear in sorted order: the first element returned is the smallest, etc.

Maps
====

A map is a *dictionary* data structure. A map contains a set of *keys*, each key being a member of the map's *key type*. Each key is associated with an arbitrary value which is a member of the map's *value type*. Duplicate keys are not allowed.

A good analogy is a phone book, which is a map from names (the key type) to phone numbers (the value type).

The **Map&lt;K, V&gt;** interface defines the map operations. (**K** is the type parameter specifying the key type, and **V** is the type parameter specifying the value type.) The most important map operations are:

{% highlight java %}
public boolean put(K key, V val); // store an association with given key,value pair
public V get(Key key);            // get the value associated with given key
public boolean removeKey(K key);  // remove key,value pair for given key
public Set<K> keySet();           // return the set of keys
{% endhighlight %}

An implementation of the map interface is expected to define efficient (O(1) or O(log N)) implementations of these methods.

There are two built-in map implementations in Java: **HashMap&lt;K, V&gt;** and **TreeMap&lt;K, V&gt;**.

For **HashMap&lt;K, V&gt;**, the **put**, **get**, and **removeKey** methods all have O(N) worst case, O(1) average case running time. The key type **K** must correctly implement the **public boolean equals(Object)** and **public int hashCode()** methods.

For **TreeMap&lt;K, V&gt;**, the **put**, **get**, and **remove** methods all have O(log N) worst case and average case running times. The key type **K** must either implement **Comparable&lt;K&gt;**, or an explicit comparator object implementing **Comparator&lt;K&gt;** must be passed to the tree map object's constructor when the tree map is created.

Data Structures
===============

This section is a high-level summary of the underlying data structures used by the built-in set and map implementations provided in Java.

A full treatment of these data structures will be provided in CS 350, Data Structures.

Hash tables
-----------

[See [course notes on hash tables](../notes/hashTables.html).]

**HashSet&lt;E&gt;** and **HashMap&lt;K, V&gt;** both use a *hash table* as the underlying data structure. A hash table works by using a *hash function* to assign *hash codes* to each key, based on the data contained in the key. The goal of the hash function is to uniformly distribute hash codes to keys, so that two different key values are unlikely to have the same hash code.

The hash table itself is typically an array of linked lists. Each linked list is a *hash bucket*. Hash buckets have the property that all of the keys contained in the bucket have hash codes such that

> *HashCode* % *NumBuckets* == *BucketIndex*

where *HashCode* is the hash code of a key in the bucket, *NumBuckets* is the number of buckets in the hash table, and *BucketIndex* is the index of the array element storing the linked list.

Assuming that the hash function does a good job at distributing keys, any particular key is equally likely to be stored in any bucket. This means that the chain of nodes in each bucket is, on average,

> N / P

where N is the total number of keys in the hash table, and P is the number of buckets.

By growing the array of buckets as more keys are added to the hash table, we can ensure that N/P is bounded by a constant. This is why, on average, set and map operations implemented using a hash table are O(1).

It is unlikely, but possible, that all keys in a hash table could be placed in the same bucket. In this case, the hash table devolves into a linked list, and the set and map operations take O(N) time.

When you write a class that will be used as a key in a HashSet or HashMap
-------------------------------------------------------------------------

There are two things that you **must** do when you write a class that will either

-   be stored in a **HashSet**
-   be used as a key in a **HashMap**

They are:

1.  You must implement the **public boolean equals(Object)** method
2.  You must implement the **public int hashCode()** method

We have seen how to write an **equals** method in [Lecture 9](lecture09.html).

The **public int hashCode()** method implements a *hash function* for the class.

To fully discuss how to write a hash function would require several lectures. The idea is that a hash function should compute an integer *hash code* that is a "summary" of the data contained in the object. There is one simple rule to follow:

> **Equal objects must have equal hash codes.**

Built-in classes (String, Integer, etc.)
----------------------------------------

More or less all of the "built-in" classes in Java, such as **String**, **Integer**, etc., have correct and efficient implementations of both **equals** and **hashCode**. So, you can use instances of these classes in instances of **HashSet** and as keys in instances of **HashMap**.

Balanced Search Trees
---------------------

See [notes on binary search trees](binarySearchTrees.html) for more information.

**TreeSet** and **TreeMap** use a *balanced search tree* as the underlying data structure.

A full discussion of search trees would take several lectures. The link above discusses *binary search trees*, which are the basis for most balanced search trees.
