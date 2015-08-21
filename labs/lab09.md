---
layout: default
title: "Lab 9: Comparable, Sorting"
---

Start by downloading [CS201\_Lab09.zip](CS201_Lab09.zip) and importing it into Eclipse. You should see a project called **CS201\_Lab09**.

Your Task
=========

Part 1 - Define a Card class
----------------------------

Define two **enum** types called **Suit** and **Rank**. The **Suit** enumeration should contain values for the suits *clubs* (lowest suit), *diamonds*, *hearts*, and *spades* (highest suit). The **Rank** enumeration should contain values for each playing card rank - two (lowest rank) through ten, jack, queen, king, then ace (highest rank).

> **Note**: specify the members of each enumeration in order from lowest to highest. I.e., **CLUBS** should be the first value in **Suit**, and **TWO** should be the first value in **Rank**. This will make it easy to compare suit and rank values.

Define a class called **Card**. An instance of **Card** represents a playing card. It should have fields to store a **Card**'s suit and rank, and a constructor to initialize them. Add getter methods to get a card's suit and rank.

Write JUnit tests to test the card class. You should create a number of **Card** objects with different suits and ranks, and test that the getter methods work on these objects.

Part 2 - Comparing Cards
------------------------

Once you have Part 1 working, change the **Card** class to implement the **java.lang.Comparable** interface. The **Card** class's **compareTo** method should compare first by suit, then by rank. So, a two of diamonds would compare as greater than an ace of clubs, because diamonds is a higher suit than clubs. Of course, three of diamonds would compare as greater than two of diamonds.

You will see a warning about **Comparable** being a raw type. Ignore this warning for now: we will see how to fix it in the next lab.

Note that enumeration types automatically implement the **Comparable** interface, so you can call the **compareTo** method on enumeration members. The comparison result will correspond to the order in which the enumeration members were defined, with earlier members comparing as less than later members.

Add some JUnit tests to test comparing **Card** objects using the **compareTo** method.

Part 3 - Sorting Cards
----------------------

Finally, demonstrate that you if you can compare cards, then an array of cards can be sorted using the **java.util.Arrays.sort** static method.

As one of the objects in your test fixture, create an array of **Card** objects. You can use the **Card** objects you've already created as element values. Make sure that the elements of the array are not already sorted.

Write a test method to sort the array. It should look something like this:

{% highlight java %}
public void testSort() {
  Arrays.sort(myArray);

  // now verify that the elements of the array are in sorted order
  assertEquals(lowestCard, myArray[0]);
  assertEquals(secondLowestCard, myArray[1]);

  // etc...
}
{% endhighlight %}

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources.html) installed, select the project (**CS201\_Lab09**) in the package explorer and then press the blue up arrow button in the toolbar. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Lab09**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **lab9**. The server URL is

> <https://cs.ycp.edu/marmoset/>
