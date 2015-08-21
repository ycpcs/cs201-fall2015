---
layout: default
title: "Lecture 8: ArrayList, Inheritance (continued)"
---

Note: The [course notes on objects, arrays, and references](../notes/objectsArraysReferences.html) will be useful.

Quick Introduction to ArrayList
===============================

ArrayList Demo Project: [arraylist-demo.zip](arraylist-demo.zip)

A common concern in Java programs is keeping track of collections of objects. *Container classes*, also known as *collections*, assist with this task: they allow your program to store collections of objects and then retrieve references to those objects when they are needed.

**ArrayList** (in the java.util package) is one of the simplest and most useful container classes. An **ArrayList** object works much like an array, but unlike an array, it has no fixed size, and expands as needed to store however many objects the program requires.

For example, let's say that you're writing a program to keep track of your friends' email addresses. You could represent the email addresses as strings, and use an **ArrayList** to store them:

{% highlight java %}
ArrayList<String> emailList = new ArrayList<String>();
{% endhighlight %}

Note that when declaring an **ArrayList** variable or creating a new **ArrayList** object, you must specify what type of objects the array list with contain. This type is called the *element type*.

To add strings to the list, call the **add** method:

{% highlight java %}
emailList.add("jane_smith@yahoo.com");
emailList.add("sally.jones@gmail.com");
emailList.add("ben456@evilhacker.com");
{% endhighlight %}

Each object added to the list is appended onto the end of the sequence of objects.

The **size** method returns an integer value specifying the number of objects currently in the list. The **get** method allows you to retrieve the object at a specified index, where 0 is the first object in the sequence, 1 is the second object, etc:

{% highlight java %}
// print all email addresses
for (int i = 0; i < emailList.size(); i++) {
    String email = emailList.get(i);
    System.out.println(email);
}
{% endhighlight %}

The **set** method takes an integer index and a reference to an object, and replaces the object at that index with the specified object. For example, if Jane Smith changes her email address, we could update our list as follows:

{% highlight java %}
String oldEmail = "jane_smith@yahoo.com";
String newEmail = "jane_smith@us.ibm.com";
for (int i = 0; i < emailList.size(); i++) {
    String email = emailList.get(i);
    if (email.equals(oldEmail)) {
        emailList.set(i, newEmail);
    }
}
{% endhighlight %}

Note that we used the **equals** method to check whether an email address string was the same as Jane's previous email address. We will discuss the **equals** method in [Lecture 9](lecture09.html).

Removing objects from a collection
----------------------------------

Sometimes, you might need to remove some number of objects from a collection. The easiest and safest way to accomplish this task is to use a temporary collection object to store the objects you want to remove, and then use the **removeAll** method to remove them from the main collection.

For example, you might be concerned that email coming from the "evilhacker.com" site contains viruses. You could purge all addresses from this site from your email list as follows:

{% highlight java %}
ArrayList<String> toRemove = new ArrayList<String>();

for (int i = 0; i < emailList.size(); i++) {
    String email = emailList.get(i);
    if (email.endsWith("@evilhacker.com")) {
        // mark this address for removal
        toRemove.add(email);
    }
}

emailList.removeAll(toRemove);
{% endhighlight %}

Inheritance of fields and methods
=================================

When a superclass defines a field or non-private method, it is *inherited* by all subclasses.

So,

-   when a superclass defines a field, the field exists in all subclass objects
-   when a superclass defines a non-private method, it may be called on an instance of any subclass

Access modifiers
================

We can specify *access modifiers* on fields and methods to restrict how they may be accessed. Java supports four access modifiers:

-   **public**: any class may access the field or method
-   **private**: only the class containing the field or method may access it
-   **protected**: like private, but subclasses may also access the field or method
-   "package-protected": if you do not explicitly specify an access modifier, it is *package-protected*. All classes in the same package may access the field or method. Curiously, subclasses may access a *package-protected* field or method, even if they are in a different package.

Even though Java supports four access modifiers, most of the time you will only use **public** and **private**.

Some rules of thumb:

-   All instance fields should be **private**.
-   All methods that are part of a class's "public interface" -the methods that perform the essential operations on instances of the class - should be **public**
-   All methods that are not part of the class's public interface should be **private**

One interesting consequence of these rules is that subclasses will not be allowed to directly access instance fields defined in the superclass. This is actually a good thing: it allows you to freely modify the fields in the superclass without affecting the subclasses in any way. (This is why **protected** fields are a bad idea - they make subclasses too sensitive to changes in the superclass.)

Defining Concrete Fields and Methods in a Superclass
====================================================

Sometimes it can be useful to define concrete (non-abstract) fields and methods in superclasses.

You should do this **only** when the field and/or methods represent properties that are truly common to all subclasses.

Example:

{% highlight java %}
public abstract class Vehicle {
    private double maxSpeed;

    public Vehicle(double maxSpeed) {
        this.speed = maxSpeed;
    }

    public double getMaxSpeed() {
        return maxSpeed;
    }

    public abstract boolean startTrip(Terrain t);
    public abstract boolean endTrip(Terrain t);
    public abstract boolean move(Terrain t);
}
{% endhighlight %}

Now all classes that inherit from the **Vehicle** superclass will have a **double** field called **maxSpeed**, and an instance method called **getMaxSpeed** which returns the value of that field.

Note that the **Vehicle** class is still abstract because it has abstract methods.

Invoking a superclass constructor from a subclass
-------------------------------------------------

When a superclass has instance fields, these fields exist in all instances of subclasses. So, constructors for subclasses will need a way to initialize these fields.

However, because instance fields are typically private, subclasses cannot access them directly. For example, here is a **Car** class that does not compile:

{% highlight java %}
public class Car extends Vehicle {
    public Car(double maxSpeed) {
        // this doesn't work because the
        // the maxSpeed field is private
        // in the Vehicle class
        this.maxSpeed = maxSpeed;
    }

    // ...definitions of startTrip, endTrip, and move methods...
}
{% endhighlight %}

The solution to this problem is for the **Car** class's constructor to call the **Vehicle** class's constructor. This is done using the **super** keyword. The call to the superclass's constructor must be the first line of code in the subclass's constructor:

{% highlight java %}
public class Car extends Vehicle {
    public Car(double maxSpeed) {
        // call superclass (Vehicle) constructor
        super(maxSpeed);
    }

    // ...definitions of startTrip, endTrip, and move methods...
}
{% endhighlight %}
