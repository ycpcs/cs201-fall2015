---
layout: default
title: "Lab 7: Inheritance and Polymorphism"
---

Start by downloading [CS201\_Lab07.zip](CS201_Lab07.zip) and importing it into Eclipse. You should see a project called **CS201\_Lab07**.

Your Task
=========

Add classes called **Boat** and **Airplane**. They should have the following behavior:

-   A legal trip for a **Boat** must start and end at a marina, and must not contain any hops over terrain other than water or marina.

-   A legal trip for an **Airplane** must start and end at an airport, but may continue through any kind of terrain.

Add new JUnit test classes called **BoatTest** and **AirplaneTest** that test **Boat** and **Airplane** objects (respectively) against both legal and illegal trips.

You can use the provided **Car** and **CarTest** classes as a guide.

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources.html) installed, select the project (**CS201\_Lab07**) in the package explorer and then press the blue up arrow button in the toolbar. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Lab07**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **lab07**. The server URL is

> <https://cs.ycp.edu/marmoset/>
