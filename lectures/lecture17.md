---
layout: default
title: "Lecture 17: Parallel Computation with Threads"
---

Exploiting Multi-core CPUs
==========================

Today's computers typically have *multi-core* CPUs. This means that they are able to execute multiple streams of instructions *simultaneously*.

We can take advantage of multiple CPU cores by creating *threads*. A thread is a stream of instructions executed within a program. One way to think of a thread is that it is a "virtual CPU". When a program has multiple threads, it has multiple virtual CPUs executing parts of the program at the same time.

Runnable
========

The **Runnable** interface describes a computational task. It is defined as follows:

{% highlight java %}
public interface Runnable {
    public void run();
}

{% endhighlight %}
When your program has a large computation to split into parts, you should define your own "computation task" class which implements the **Runnable** interface. Your program will create one instance of your task class for each "chunk" of the computation.

Thread
======

The **Thread** class represents a thread (virtual CPU). A thread takes a reference to an object implementing the **Runnable** interface, and executes its **run** method in a separate thread.

There are three important **Thread** methods that you will use.

The **Thread** class's constructor takes a reference to the **Runnable** object whose **run** method you want the new thread to execute. Note that creating the **Thread** object does not actually start the thread.

The **Thread** class's **start** method actually starts a new thread. The new thread will execute the **run** method of the **Runnable** object passed to the **Thread**'s constructor.

The **Thread** class's **join** method can be called to wait for the thread to complete. In other words, the **join** method returns after the **Runnable** object's **run** method returns.

Note that the **join** method can throw a checked exception called **InterruptedException**.

Fork/Join Parallelism
=====================

A very common pattern for parallel computation is *fork/join parallelism*. In programs that employ this form of computation, the main program creates some number of parallel "worker" threads, starts them, and then waits for all of them to complete.

Here is how fork/join parallelism can be implemented in Java. This code example assumes that there is a class called **ComputeTask** that implements the **Runnable** interface and carries out a given chunk of the computation. This example creates 4 threads, allowing parallel computation on up to 4 CPU cores simultaneously.

{% highlight java %}
// Split the computation into 4 tasks
ComputeTask[] tasks = new ComputeTask[4];
for (int i = 0; i < 4; i++) {
    tasks[i] = new ComputeTask(...data that describes the task...);
}

// create the threads that will execute the tasks,
// and start each thread
Thread[] threads = new Thread[4];
for (int i = 0; i < 4; i++) {
    threads[i] = new Thread(tasks[i]);
    threads[i].start();
}

// wait for all of the threads to complete
try {
    for (int i = 0; i < 4; i++) {
        threads[i].join();
    }
} catch (InterruptedException e) {
    // this should not happen
    System.err.println("A thread was interrupted");
}

// Now, we can look at the results of each compute task,
// and combine them into a single overall result
{% endhighlight %}

Communication Between Threads
=============================

In fork/join parallelism, the computation threads are completely independent of each other. This is the ideal case for a parallel computation: each parallel task does not need to communicate with any other parallel task. Such parallel computations tend to be easy to implement, and execute very efficiently.

Some parallel computations, however, require *communication* between computation tasks. Threads executing in parallel can communicate with each other using a *shared data structure*. For example, a queue (list) could be used to communicate values from one thread to the next.

When a data structure is shared between threads, some form of *synchronization* must be used to ensure that the threads are not accessing and modifying the data structure at the same time. We will not be investigating thread synchronization in this course, but the basic idea is that "locks" can be used to temporarily give one thread exclusive access to the shared data structure.

(If you are interested in learning more, do a web search for "mutex", "critical section", and "java synchronization".)
