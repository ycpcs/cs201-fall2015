---
layout: default
title: "Lab 8: Inheriting Fields and Methods"
---

Getting Started
===============

Download [CS201\_Lab08.zip](CS201_Lab08.zip) and import it into your Eclipse workspace (**File&rarr;Import&rarr;General&rarr;Existing projects into workspace&rarr;Archive file**.) You should see a project called **CS201\_Lab08** in the Package Explorer.

Right click on **StartLab.java** and choose **Run As&rarr;Java Application**. In the console window, type **yes** when prompted. When the program completes, right click on the project (**CS201\_Lab08**) and choose **Refresh**. You should see your code from [Lab 7](lab7.html).

In this lab, you will add the capability to the classes in the **Vehicle** class hierarchy to represent the vehicle's maximum speed, and use this feature to add a capability to the **Trip** class to determine a vehicle's average speed on a particular trip.

Your Task
=========

Make the following modifications:

**(1)** Add a **maxSpeed** field, with type **double**, in the **Vehicle** class. Add a constructor to **Vehicle** that takes a single **double** parameter and uses its value to initialize the **maxSpeed** parameter.

**(2)** Add a **getMaxSpeed** accessor method to **Vehicle** to return the **Vehicle's** maximum speed.

**(3)** Add constructors to **Car**, **Boat**, and **Airplane** taking a single **double** parameter. Each constructor should call the superclass constructor, passing the parameter value as the argument.

**(4)** Add the following abstract method to the **Vehicle** class:

    public abstract double getSpeed(Terrain t);

This method returns the speed of the **Vehicle** over the given kind of terrain. You will need to implement this method in each subclass of **Vehicle**.

Here are the rules for different kinds of vehicles:

-   A **Car** moves at its maximum speed over **ROAD** terrain, and at one-quarter of its maximum speed over **AIRPORT** and **MARINA** terrain.

-   A **Boat** moves at its maximum speed over **WATER**, and at one-quarter of its maximum speed over **MARINA**.

-   An **Airplane** moves at its maximum speed over all kinds of terrain.

If the **getSpeed** method is called with a terrain type that is not legal for a particular kind of **Vehicle**, you can throw an **IllegalArgumentException**:

    throw new IllegalArgumentException("Illegal terrain: " + t);

**(5)** Your JUnit test classes will no longer compile because they assume that **Car**, **Boat**, and **Airplane** objects can be created without passing any arguments to the constructor. Change these tests so that:

-   The **Car** object has a maximum speed of 100.
-   The **Boat** object has a maximum speed of 50.
-   The **Airplane** object has a maximum speed of 500.

Re-run all of the tests to make sure they still pass.

**(6)** Add the following method to the **Trip** class:

{% highlight java %}
public double findAverageSpeed(Vehicle v) {
    ...
{% endhighlight %}

This method determines the average speed of a given **Vehicle** traversing the sequence of terrain represented by the **Trip** object on which the method is called, assuming that the vehicle always moves at its maximum speed. It should compute the total time required for the trip. Let's say that the trip is composed of terrain types

> *t*<sub>0</sub>, *t*<sub>1</sub>, *t*<sub>2</sub>, ..., *t*<sub>n-1</sub>

The max speed of a vehicle over terrain value *t* is

> speed(*t*)

which is what is returned by calling the **getSpeed** method on the vehicle object and passing the terrain value *t*.

The total amount of time *T* required for the trip is

> *T* = (1 / speed(*t*<sub>0</sub>)) + (1 / speed(*t*<sub>1</sub>)) + (1 / speed(*t*<sub>2</sub>)) + ... + (1 / speed(*t*<sub>n-1</sub>))

Then, the average speed for the trip is

> *n* / *T*

**(7)**. Add JUnit tests to **CarTest**, **BoatTest**, and **AirplaneTest** to test the **getSpeed** and **findAverageSpeed** methods.

For example:

{% highlight java %}
// in CarTest

private static final double DELTA = 0.00001;

private Trip exampleTrip;
private Car myCar;

protected void setUp() {
  exampleTrip = new Trip(3);
  exampleTrip.setHop(0, Terrain.AIRPORT);
  exampleTrip.setHop(1, Terrain.ROAD);
  exampleTrip.setHop(2, Terrain.MARINA);

  myCar = new Car(100.0); // the Car's maximum speed is 100
}

public void testGetSpeed() {
  // full speed over road
  assertEquals( 100.0, myCar.getSpeed(Terrain.ROAD), DELTA );

  // one-quarter speed through an airport
  assertEquals( 0.25 * 100.0, myCar.getSpeed(Terrain.AIRPORT), DELTA );

  // one-quarter speed through a marina
  assertEquals( 0.25 * 100.0, myCar.getSpeed(Terrain.MARINA), DELTA );
}

public void testFindAverageSpeed() throws Exception {
  double dist = 3.0;
  double time = (1.0/(.25 * 100.0)) + (1.0 / 100.0) + (1.0 / (.25 * 100.0));
  assertEquals( dist /  time, exampleTrip.findAverageSpeed(myCar), DELTA);
}
{% endhighlight %}

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources.html) installed, select the project (**CS201\_Lab08**) in the package explorer and then press the blue up arrow button in the toolbar. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Lab08**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **lab08**. The server URL is

> <https://cs.ycp.edu/marmoset/>
