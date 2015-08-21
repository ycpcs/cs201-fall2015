---
layout: default
title: "Lab 10: Using Generic Containers and Algorithms"
---

Getting Started
===============

This lab will use your code from [Lab 9](lab09.html) as a starting point.

Download [CS201\_Lab10.zip](CS201_Lab10.zip) and import it into your Eclipse workspace (**File&rarr;Import&rarr;General&rarr;Existing projects into workspace&rarr;Archive file**.) You should see a project called **CS201\_Lab10** in the Package Explorer.

Right click on **StartLab.java** and choose **Run As&rarr;Java Application**. In the console window, type **yes** when prompted. When the program completes, right click on the project (**CS201\_Lab10**) and choose **Refresh**. You should see your code from [Lab 9](lab09.html).

Your Task
=========

**(1)** Modify your **Card** class so that rather than implementing the **Comparable** interface, it implements **Comparable\<Card\>**: instead of

{% highlight java %}
public class Card implements Comparable {
{% endhighlight %}

use

{% highlight java %}
public class Card implements Comparable<Card> {
{% endhighlight %}

Change the type of the **compareTo** method's parameter from **Object** to **Card**. You can now take out the type cast you used to convert the **Object** reference into a **Card** reference.

Run your JUnit tests again to make sure everything still works correctly.

**(2)** Add an **equals** method to the **Card** class. Add JUnit tests to **CardTest** to make sure it works properly.

**(3)** Implement the **Deck** class. It should look like this:

{% highlight java %}
public class Deck {
    // fields

    public Deck() {
        // generate a full deck (52 cards)
    }

    public int getNumCards() {
        // return number of cards in the deck
    }

    public Card getCard(int i) {
        // return the i'th card in the deck
    }

    public Card drawCard() {
        // draw a Card from the top of the deck
        // and return a reference to it
    }

    public void shuffle() {
        // randomly shuffle the deck
        // use the Collections.shuffle() static method!
    }
}
{% endhighlight %}

Use an **ArrayList\<Card\>** (ArrayList of Cards) to store the cards.

The **get** method could use the **get** method of **ArrayList\<Card\>**.

The **drawCard** method could use the **remove(int)** method of **ArrayList\<Card\>**. (Use it to remove the last card in the list of cards, and return a reference to the removed card.)

Add a JUnit test class called **DeckTest**. It should contain tests for the **getNumCards**, **drawCard**, and **Shuffle** methods of the **Deck** class.

Hints
=====

You can iterate through all of the elements of an enumeration by calling the enumeration's **values** static method, which returns an array. For example, this code snippet should be useful in the **Deck** constructor:

{% highlight java %}
Suit[] allSuits = Suit.values();
Rank[] allRanks = Rank.values();

for (int j = 0; j < allSuits.length; j++) {
    for (int i = 0; i < allRanks.length; i++) {
        // use allSuits[j] and allRanks[i] to create a Card
    }
}
{% endhighlight %}

You can implement the **Deck** class's **shuffle** method by calling **Collections.shuffle**, passing the collection containing the **Deck** object's **Cards** as a parameter. In your JUnit test for **shuffle**, verify that at least some of the cards in the deck changed position.

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources.html) installed, select the project (**CS201\_Lab10**) in the package explorer and then press the blue up arrow button in the toolbar. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Lab10**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **lab10**. The server URL is

> <https://cs.ycp.edu/marmoset/>
