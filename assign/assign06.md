---
layout: default
title: "Assignment 6: Web Crawler"
---

**Due**: Tuesday, December 15th by 11:59 PM

Getting Started
===============

Download [CS201\_Assign06.zip](CS201_Assign06.zip) and import it into your Eclipse workspace.

You should see a project named **CS201\_Assign06**.

Your Task
=========

You have two tasks:

1.  Implement the static methods defined in the **URI** class, described below. You can use the **URITest** test class to test them.
2.  Implement the **main** method in the **WebCrawler** class.

See the **URIs** and **Web Crawler** sections below for details.

URIs
====

A URI (Uniform Resource Identifier) is a string which identifies the location of a web page.

The **URI** class contains static methods which operate on URI strings. The **URITest** class contains JUnit tests which check whether or not these methods are implemented correctly. A documentation comment explains precisely how each method is supposed to work.

In this assignment, we will use file names as URIs. This will allow us to implement a web spider that performs a web crawl of HTML files in the local filesystem.

Example file name URIs:

> index.html
>
> foo/bar/
>
> foo/bar/baz.html
>
> foo/bar/./baz.html
>
> foo/bar/thud/../baz.html
>
> /www/somePage.html

A URI can be *relative* or *absolute*. A URI that begins with a "/" character is absolute. All other URIs are relative. For example, "index.html" and "foo/bar/" are relative URIs, while "/www/somePage.html" is an absolute URI.

A directory URI is one which ends with a "/" character, or which is the empty string "". For any URI, we can extract its directory part as follows:

-   if a URI does not contain any "/" characters, then its directory part is "" (the empty string)
-   if a URI does contain at least one "/" character, then its directory part is the prefix of the string which ends in the last occurrence of "/"

For example, the directory part of "index.html" is "", and the directory part of "/www/somePage.html" is "/www/".

A URI is in canonical form if it does not contain any "." or ".." components. A "." component means "the current directory", while a ".." component means "the parent directory". Therefore the three URIs

> foo/bar/baz.html
>
> foo/bar/./baz.html
>
> foo/bar/thud/../baz.html

all have the same canonical form, which is "foo/bar/baz.html". Being able to convert a URI to canonical form is important, because it ensures that the web spider will be able to detect when it encounters a page visited previously.

When one web page (the "base" page) contains a link to another web page (the "referenced" page), the URI of the referenced page may be relative. In this case, the complete URI of the referenced page is determined by extracting the directory from the base page, and appending the URI of the referenced page. For example, if the URI "foo/bar/baz.html" is referenced from the page "/www/somePage.html", the complete URI of the referenced page is "/www/foo/bar/baz.html".

Web Crawler
===========

The **main** method of the **WebCrawler** class implements the web crawler. It reads from the keyboard the name of a directory, and the URI of a starting web page within that directory. It then scans the start web page, and all other web pages linked directly and indirectly from the start web page.

The output of the **WebCrawler** class's **main** method should be

-   a list of pages visited
-   a list of broken links: links found in scanned HTML documents which referred to missing files (including the page in which each broken link occurred, along with the full URI of the nonexistent web page)

A directory named **exampleSite** contains some test web pages that you can use to test your web crawler. Example run (user input in **bold**):

<pre>
Enter directory: <b>exampleSite</b>
Enter starting web page URI: <b>/index.html</b>
Visited web pages:
  /index.html
  /coolStuff.html
  /info/resources.html
  /lizards.html
  /info/books.html
  /info/music.html
  /info/pictures/gallery.html
  /monitorLizards.html
  /secret.html
Broken links:
  /news/notThere.html, linked from /coolStuff.html
  /info/moreResources.html, linked from /info/resources.html
  /komodoDragons.html, linked from /lizards.html
</pre>

Note that the order in which your crawler prints visited pages and broken links is not important. However, it should report the same pages and broken links listed above.

Converting URIs to Filenames
----------------------------

The starting web page will be designated by an absolute URI (one that begins with a "/".) You can convert this URI to a filename by appending it to the directory entered by the user. For example, if the user enters

    exampleSite

as the directory and

    /index.html

as the starting web page URI, then the filename for the starting web page will be

    exampleSite/index.html

When the web crawler finds links from the starting web page to other web pages, it should compute absolute URIs for the linked web pages by calling the **getReferencedURI** method. The absolute URIs can then be converted to filenames the same way as the starting web page.

Crawling Web Pages
------------------

Starting from the start web page, the web crawler should search each web page it encounters for links to other pages. You may assume that any occurrence of text matching the pattern

<pre>
href="<i>...URI of web page...</i>"
</pre>

is a link to another page.

The web crawler should maintain a queue of the URIs of web pages that need to be visited. Whenever the web crawler encounters a link to a web page it has not yet scanned, it should add the page's URI to the queue.

To avoid visiting the same page multiple times, the web crawler should use a map or set to keep track of the pages it has encountered.

Hints
=====

In the **makeCanonical** method of the **URITest** class, you will need to extract each component of the URI in order. For example, the components of the URI "foo/bar/baz.html" are "foo", "bar", and "baz.html".

You can do so with the following code

{% highlight java %}
while ( ! uri.equals("") ) {

    int slash = uri.indexOf('/');

    String component;
    if (slash >= 0) {
    	component = uri.substring(0, slash);
    	uri = uri.substring(slash + 1);
    } else {
    	component = uri;
    	uri = "";
    }

    // ...do something with the URI component, using a stack...
}
{% endhighlight %}

Note that a URI can contain multiple occurrences of the ".." component: e.g.,

> foo/bar/baz/../../x.html

since the ".." component means "go back to parent directory", the canonical form of this URI is

> foo/x.html

A stack of URI component strings will help you find the canonical form of the URI you are processing.

Note that when converting a URI into its canonical form, any leading and/or trailing occurrences of the slash ("/") character must be preserved.

Grading
=======

-   URI methods: 40%
-   Extracting links from visited web pages: 20%
-   Visiting all pages: 20%
-   Detecting broken links: 20%

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

> **Important**: after you submit, log into the submission server and verify that the correct files were uploaded. You are responsible for ensuring that you upload the correct files. I may assign a grade of 0 for an incorrectly submitted assignment.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources.html) installed, select the project (**CS201\_Assign06**) in the package explorer and then press the blue up arrow button in the toolbar. Enter your Marmoset username and password when prompted.

From a web browser
------------------

Save the project (**CS201\_Assign06**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **assign06**. The server URL is

> <https://cs.ycp.edu/marmoset/>
