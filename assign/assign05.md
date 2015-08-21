---
layout: default
title: "Assignment 5: Mandelbrot Set Renderer"
---

**Due**: Thursday, July 23rd by 11:59 PM

Getting Started
===============

Download [CS201\_Assign05.zip](CS201_Assign05.zip) and import it into your Eclipse workspace (**File&rarr;Import&rarr;General&rarr;Existing projects into workspace&rarr;Archive file**.)

You should see a project called **CS201\_Assign05** in the Package Explorer. Your will be making changes to the **main** method of the **Mandelbrot** class. You should add any additional classes or methods needed to complete the program.

Your Task
=========

Your task is to implement a renderer for the [Mandelbrot Set](http://en.wikipedia.org/wiki/Mandelbrot_set), using [parallel computation](../lectures/lecture17.html) to speed up the rendering process.

> ![Exploit all the cores!](images/assign05/exploitAllTheCores.jpg)
> <br>Apologies to [Allie Brosh](http://hyperboleandahalf.blogspot.com/)

The program should prompt the user for a pair of x,y coordinates specifying corners of a rectangle in the x/y plane. The program should also prompt the user to enter the name of a file ending with the ".png" file extension. Once this input has been entered, the program should render a 600 pixel by 600 pixel image which visualizes the specified region of the Mandelbrot set.

Example session (user input in **bold**):

<pre>
Please enter coordinates of region to render:
  x1: <b>-1.286667</b>
  y1: <b>-0.413333</b>
  x2: <b>-1.066667</b>
  y2: <b>-0.193333</b>
Output filename: <b>output.png</b>
Working...
Output file written successfully!
</pre>

The output file generated should be a PNG image file that looks something like this (click to see larger version):

> <a href="images/assign05/output.png"><img style="width: 300px; height: 300px;" src="images/assign05/output.png" /></a>

The exact appearance of the image will depend on how you choose to map the number of iterations at the sampled points to colors. See the next section for details.

The Mandelbrot Set
==================

The Mandelbrot set is a fractal: a mathematical object that is self-similar at all scales. It is defined as follows:

-   Each point on the x/y plane is interpreted as a [complex number](http://en.wikipedia.org/wiki/Complex_number), where x is the real part and y is the imaginary part.

-   A point (x,y) is considered to be in the set if, for its corresponding complex number C the equation

    > Z<sub>n+1</sub> = (Z<sub>n</sub>)<sup>2</sup> + C

    can be iterated any number of times without the magnitude of Z ever becoming greater than 2.0. The initial value of Z (Z<sub>0</sub>) is (0+0i).

Note that the magnitude of a complex number is the square root of the sum of the squares of its real and imaginary components. See the Wikipedia article linked above for an explanation of how to add and multiply complex numbers.

Important Hint
--------------

Because the core computation is based on complex numbers, having a class to represent complex numbers will make implementing the computation much easier. The class should look something like this:

{% highlight java %}
public class Complex {
    // ...fields...

    // Constructor
    public Complex(double real, double imag) {
        // ...
    }

    // add given complex number to this one, returning the Complex result
    public Complex add(Complex other) {
        // ...
    }

    // multiply given complex number by this one, returning the Complex result
    public Complex multiply(Complex other) {
        // ...
    }

    // get the magnitude of this complex number
    public double getMagnitude() {
        // ...
    }
}
{% endhighlight %}

You will need to think about what fields to add and how to implement each operation.

Once your **Complex** class is ready, you can iterate the equation as follows:

{% highlight java %}
z = z.multiply(z).add(c);
{% endhighlight %}

This assumes that you have variables **z** and **c** that refer to instances of the **Complex** class.

Creating a task class
---------------------

You should create a task class that computes the iteration counts for a region of the image.

Here is a suggested skeleton:

{% highlight java %}
public class MandelbrotTask implements Runnable {
    private double x1, y1, x2, y2;
    private int startCol, endCol, startRow, endRow;
    private int[][] iterCounts;

    public MandelbrotTask(double x1, double y1, double x2, double y2,
                          int startCol, int endCol, int startRow, int endRow,
                          int[][] iterCounts) {
        this.x1 = x1;
        this.y1 = y1;
        this.x2 = x2;
        this.y2 = y2;
        this.startCol = startCol;
        this.endCol = endCol;
        this.startRow = startRow;
        this.endRow = endRow;
        this.iterCounts = iterCounts;
    }

    public void run() {
        for (int i = startRow; i < endRow; i++) {
            for (int j = startCol; j < endCol; j++) {
                Complex c = getComplex(i, j);
                int iterCount = computeIterCount(c);
                iterCounts[i][j] = iterCount;
            }
        }
    }

    // TODO: implement getComplex and computeIterCount methods
}
{% endhighlight %}

The idea is that a **MandelbrotTask** object will compute iteration counts for the region of the image with rows from **startRow** (inclusive) to **endRow** (exclusive) and columns from **startCol** (inclusive) to **endCol** (exclusive). The region of the complex plane is specified by **x1**, **y1**, **x2**, and **y2**.  The **iterCounts** array is the single global array used to store the iteration counts for the overall image (where the first dimension is rows and the second dimension is columns).

From the **main** method, you could use a **MandelbrotTask** object to compute all of the iteration counts as follows:

{% highlight java %}
int[][] iterCounts = new int[HEIGHT][WIDTH];
MandelbrotTask task = MandelbrotTask(x1, y1, x2, y2, 0, WIDTH, 0, HEIGHT, iterCounts);
task.run();
{% endhighlight %}

Note that this approach is purely sequential, and will not take advantage of multiple CPU cores.

Rendering the Mandelbrot Set
============================

Rendering the Mandelbrot set is done by assigning a color to sampled points in a region of the x/y plane.

Points that are in the Mandelbrot set should be rendered as black.

Points that are outside the Mandelbrot set should be rendered using a color that indicates how many times the equation was iterated before the magnitude of Z reached 2.0. In my implementation, purple is used for points where the magnitude of Z reached 2.0 in 1 iteration. Then, as higher numbers of iterations are needed for the magnitude of Z to reach 2.0, my renderer chooses colors that transition smoothly from purple, to blue, to green, to yellow, to orange, and last to red (for points that are very close to the set, but not within it.)

You may choose any assignment of colors to numbers of iterations, as long as the each color is based on the number of iterations.

So, the 600 by 600 image you render will pick sample points uniformly spaced in a 600 by 600 grid which overlays the region of the x/y plane specified by the user, and set an image color for each corresponding pixel based on whether or not the point is in the set, and if not, how many iterations were required to show that it is not in the set.

Rendering An Image, Saving It
=============================

The Java **BufferedImage** class allows you to render an image:

{% highlight java %}
BufferedImage bufferedImage = new BufferedImage(WIDTH, HEIGHT, BufferedImage.TYPE_INT_ARGB);
Graphics g = bufferedImage.getGraphics();

// ... use g to perform drawing operations ...

g.dispose();
{% endhighlight %}

Once the image has been rendered into the **BufferedImage** object, you can write it to a file as follows:

{% highlight java %}
OutputStream os = new BufferedOutputStream(new FileOutputStream(fileName));
try {
    ImageIO.write(bufferedImage, "PNG", os);
} finally {
    os.close();
}
{% endhighlight %}

Parallelism
===========

The computation performed by the program can take a fair amount of CPU time. However, the computation of the number of iterations for each point is *independent* of the computations for all other points. Therefore, you can speed the program up by using multiple threads to compute the number of iterations in different parts of the overall region.

For example, you might divide the overall region into quadrants, and use a separate thread to compute the points in each quadrant. Since there are four threads, if you run the program on a computer with 4 CPU cores, then you could see up to a 4 times speedup.  (Question: is this the best approach for dividing up the work?)

**Suggestion**: Create multiple **MandelbrotTask** objects, and execute each one in a separate thread.

Grading Criteria
================

Your submission will be graded according to the following criteria:

- Computation: 40%
- Basic rendering of image: 20%
  * Smooth interpolation of colors (extra credit): 5%
- Use of threads for parallelism: 30%
- Design, coding style: 10%

Insane Extra Credit
-------------------

For up to 50 points of extra credit, implement an interactive GUI.  The GUI should start by visualizing the region (-2,-2) to (2,2).  The user should be allowed to zoom in on an arbitrary square region.

**Important**: The GUI should do the computation in a separate thread, not in the event loop thread.  In otherwords, do *not* do the computation directly in an event handler.  Instead, when a new rendering needs to be performed, the event handler should start a thread to do the computation.  When the computation is done, it should use **SwingUtilities.invokeLater** to schedule some code to run in the event loop, which then should cause the view to be updated.

Come see me for some suggestions on how to approach the GUI.

Make sure that you have the sequential and parallel computation working before you try creating a GUI.

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

> **Important**: after you submit, log into the submission server and verify that the correct files were uploaded. You are responsible for ensuring that you upload the correct files. I may assign a grade of 0 for an incorrectly submitted assignment.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources.html) installed, select the project (**CS201\_Assign05**) in the package explorer and then press the blue up arrow button in the toolbar. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Assign05**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **assign05**. The server URL is

> <https://cs.ycp.edu/marmoset/>
