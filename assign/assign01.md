---
layout: default
title: "Tic Tac Toe"
---

**Due**: Friday, September 11th by 11:59 PM

# Getting Started

Download [CS201\_Assign01.zip](CS201_Assign01.zip) and import it into your Eclipse workspace (**File &rarr; Import &rarr; General &rarr; Existing projects into workspace &rarr; Archive file**.)

You should see a project called **CS201\_Assign01** in the Package Explorer.

You can run the program interactively by right-clicking on **TicTacToe.java** and choosing **Run As &rarr; Java Application**.

# Your Task

In this assignment, you will complete the implementation of a Tic-Tac-Toe program.

## Example Session

Here is an example session (user input in **bold**):

<pre>
   |   |   
---|---|---
   |   |   
---|---|---
   |   |   

Player X's turn:
Enter row (0-2): <b>1</b>
Enter column (0-2): <b>1</b>

   |   |   
---|---|---
   | X |   
---|---|---
   |   |   

Player O's turn:
Enter row (0-2): <b>0</b>
Enter column (0-2): <b>0</b>

 O |   |   
---|---|---
   | X |   
---|---|---
   |   |   

Player X's turn:
Enter row (0-2): <b>4</b>
Enter column (0-2): <b>2</b>
Invalid move, try again

 O |   |   
---|---|---
   | X |   
---|---|---
   |   |   

Player X's turn:
Enter row (0-2): <b>1</b>
Enter column (0-2): <b>1</b>
Invalid move, try again

 O |   |   
---|---|---
   | X |   
---|---|---
   |   |   

Player X's turn:
Enter row (0-2): <b>0</b>
Enter column (0-2): <b>1</b>

 O | X |   
---|---|---
   | X |   
---|---|---
   |   |   

Player O's turn:
Enter row (0-2): <b>2</b>
Enter column (0-2): <b>1</b>

 O | X |   
---|---|---
   | X |   
---|---|---
   | O |   

Player X's turn:
Enter row (0-2): 
</pre>

# Requirements and Specifications

The **main** method is provided for you.  You won't need to change it.

Your task is to complete the static methods described below.  Static methods are like C functions, so this assignment will be very much like writing a C program.

The game board is represented by a 3x3 array of **int** values:

{% highlight java %}
int[][] board = new int[3][3];
{% endhighlight %}

Note that each element of the array will contain the value 0 initially.

The first dimension of the array is the rows of the board, and the second dimension is the columns.  Each array element represents a location on the game board.  The values of the elements are interpreted as follows:

* 0 indicates a blank space
* 1 indicates a space with an **X**
* 2 indicates a space with an **O**

The **PLAYER\_X** and **PLAYER\_O** constants are defined with the values 1 and 2, respectively.  You should use these constants as apporpriate in the program.

Make sure that your program's output matches the output shown above as closely as possible.  In particular, make sure that all prompts and messages are spelled correctly.

## Static methods

These are the static methods you must implement.

Note that the bodies of some of the methods have the code

{% highlight java %}
throw new UnsupportedOperationException("not implemented yet");
{% endhighlight %}

As you implement each method, simply remove this code.

Also note that arrays in Java are passed by reference (just like arrays in C), so a static method can modify an array it receives via a parameter.

<dl>
<dt><b>public static void printBoard(int[][] board)</b></dt>
<dd>
This method prints a representation of the board.
</dd>

<dt><b>public static int getRow(Scanner keyboard)<br>public static int getCol(Scanner keyboard)</b></dt>
<dd>
These methods should prompt the user to enter row and column values, reading them with the <b>Scanner</b> passed as the parameter.  The value entered by the user should be returned as the result.  Note that these methods don't need to check the value entered by the user for validity.
</dd>

<dt><b>public static boolean isLegalMove(int[][] board, int row, int col)</b></dt>
<dd>
This method checks the specified row and column to see if they constitute a legal move.  A move is legal if the row and column are each in the range 0-2 (inclusive) and if the board contains a blank space (0 value) at that position.  The method should return <b>true</b> if the move is legal, and <b>false</b> if the move is not legal.
</dd>

<dt><b>public static void placeMarker(int[][] board, int row, int col, int player)</b></dt>
<dd>
This method should place the given player's marker on the board at the specified row and column.
</dd>

<dt><b>private static boolean playerWins(int[][] board, int player)</b></dt>
<dd>
This method should return <b>true</b> if the specified player has won the game by getting three pieces in a row in a row, column, or diagonal, and <b>false</b> if the player has not won the game.
</dd>

<dt><b>private static boolean isDraw(int[][] board)</b></dt>
<dd>
This method should return <b>true</b> if all spaces on the board are occupied and <b>false</b> if there is at least one empty space on the board.
</dd>

</dl>

## Testing

You can run JUnit tests by right-clicking **TicTacToeTest.java** (in the **junit** source folder) and choosing **Run As &rarr; JUnit test**.  If you see a green bar, then all of the tests have passed.

Note that not every method will be tested, and it is possible that the tests don't test every possible situation.  I highly encourage you to add your own tests!

# Grading

The assignment will be graded as follows:

* printBoard - 15%
* getRow, getCol - 10%
* isLegalMove - 20%
* placeMarker - 5%
* playerWins - 20%
* isDraw - 20%
* coding style - 10%

# Submitting

When you are done, submit the lab to the Marmoset server using either of the methods below.

> **Important**: after you submit, log into the submission server and verify that the correct files were uploaded. You are responsible for ensuring that you upload the correct files. I may assign a grade of 0 for an incorrectly submitted assignment.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources.html) installed, select the project (**CS201\_Assign01**) in the package explorer and then press the blue up arrow button in the toolbar. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Assign01**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **assign01**. The server URL is

> <https://cs.ycp.edu/marmoset/>
