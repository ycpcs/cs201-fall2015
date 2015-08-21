---
layout: default
title: "Lecture 6: GUIs"
---

GUIs
====

We will be doing several programming assignments involving the creation of simple GUIs. Here is a quick overview of how GUIs work in Java.

Events
------

Programs which have a graphical user interface are *event-driven*. That means that the program does not "do anything" unless an event occurs. Example of events are things like

-   mouse clicks
-   moving the mouse
-   pressing a button

The program responds to events by establishing a *handler* for the event. An event handler is simply a method which is called whenever the event occurs. Handlers are specific to a particular window or GUI component. For example, if your program has multiple windows, then you will probably have one handler for each window.

Writing an event-driven program takes a bit of getting used to. The basic idea is that the program has *state variables* which store the current "state" of the program. Events can use and modify the state variables to respond to events as they occur.

Frames and Panels
-----------------

A *frame* is a top-level window. Generally, a frame is only used as a container for other GUI components. In Java, an instance of the **JFrame** class represents a frame.

A *panel* is a rectangular region of a window. Panels are often used as a container for components such as buttons, text boxes, etc. Another use for panels is as a surface for drawing graphics; this is the way we will usually be using panels in this course. In Java, an instance of the **JPanel** class represents a panel.

paint() and repaint()
---------------------

To use a **JPanel** instance for drawing graphics, you can do the following:

-   create your own class as a subclass of **JPanel**
-   define a method called **paint** in your subclass

The **paint** method will be called whenever the contents of your panel need to be redrawn. Note that drawing is event-driven; a call to the **paint** method is made automatically whenever a "window expose" event occurs, where a previously-hidden area of the panel becomes visible.

A **paint** method looks like this:

{% highlight java %}
public void paint(Graphics g) {
    ...
{% endhighlight %}

The parameter is a reference to an object whose type is **java.awt.Graphics**. A **Graphics** object has a large number of methods to perform drawing operations within whatever component is being drawn (e.g., the contents of your panel).

Example: drawing a solid blue rectangle:

{% highlight java %}
g.setColor(Color.BLUE);
g.fillRect(100, 75, 200, 100);
{% endhighlight %}

The rectangle drawn by the code above has its upper-left corner at position x=100, y=75, is 200 pixels wide, and 100 pixels high. Note that in Java graphics, y coordinates increase towards lower points on the screen (i.e., going down).

If, in response to an event, you would like to *force* your panel to be redrawn, simply call the **repaint** method. This method takes no arguments.

A complete example
------------------

As a simple example program, we will implement a GUI application which displays an integer count. Each time the mouse is clicked, the count increases. Mouse clicks also cause a rectangle displayed in the window to change color.

The comments in the example explain what the code is doing.

Here is the **CountFrame** class:

{% highlight java %}
package edu.ycp.cs201.guiexample;

import javax.swing.JFrame;
import javax.swing.SwingUtilities;

public class CountFrame extends JFrame {
    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                CountFrame frame = new CountFrame();

                // embed a CountPanel in the frame
                frame.add(new CountPanel());

                // "packing" the frame causes it to adjust its size based
                // on the panel's preferred size
                frame.pack();

                // when the frame is closed, exit the program
                frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

                // making the frame visible starts the program
                frame.setVisible(true);
            }
        });
    }
}
{% endhighlight %}

There is no important behavior in the **CountFrame** class -it is simply a container for a **CountPanel**, which is where everything interesting will happen.

Here is the **CountPanel** class:

{% highlight java %}
package edu.ycp.cs201.guiexample;

import java.awt.Color;
import java.awt.Dimension;
import java.awt.Font;
import java.awt.Graphics;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;

import javax.swing.JPanel;

public class CountPanel extends JPanel {
    // constants defining the preferred width and height of the panel
    private static final int WIDTH = 400;
    private static final int HEIGHT = 300;

    // this font will be used to display the count
    private static final Font font = new Font("Dialog", Font.BOLD, 48);

    // as the count increases, the rectangle will cycle through these colors
    private static final Color[] colors = { Color.RED, Color.GREEN, Color.BLUE };

    // field storing the current count
    private int count;

    // constructor
    public CountPanel() {
        count = 0;

        setBackground(Color.GRAY);

        setPreferredSize(new Dimension(WIDTH, HEIGHT));

        // install event handlers
        addMouseListener(new MouseAdapter() {
            @Override
            public void mouseClicked(MouseEvent e) {
                handleMouseClick(e);
            }
        });
    }

    private void handleMouseClick(MouseEvent e) {
        // change the "state" of the program
        count++;

        // now that the state is changed,
        // redraw the panel to reflect the state change
        repaint();
    }

    @Override
    public void paint(Graphics g) {
        super.paint(g); // call the superclass's paint() method to paint the background

        // draw the rectangle
        g.setColor(colors[count % colors.length]);
        g.fillRect(20, 20, WIDTH - 40, HEIGHT - 40);

        // draw the count
        g.setFont(font);
        g.setColor(Color.WHITE);
        g.drawString("" + count, 50, 150);
    }
}
{% endhighlight %}

The most important thing to think about as you look at this code is the event-driven nature. The **count** field is the "state" of the program. Mouse click events cause this state to change. When the state changes, the panel is redrawn to reflect the state change.

Here is the code as an Eclipse project:

> [lecture6-guiexample.zip](lecture6-guiexample.zip)

Here is a much better example project using a Model/View/Controller architecture:

> [mvc-gui-demo.zip](mvc-gui-demo.zip)
