Documentation (JavaDoc)
=======================

Our Javadoc guidelines are loosely based on `Stephen Colebourne's blog article on Javadoc coding standards <http://blog.joda.org/2012/11/javadoc-coding-standards.html>`_ 
and `Oracle's guide on writing Javadoc <http://www.oracle.com/technetwork/java/javase/documentation/index-137868.html>`_. 
Note that these guidelines merely specify the layout and formatting of the documentation but not its content.

General Formatting
------------------
A Javadoc comment is written in HTML and can therefore use common HTML tags. 
A JavaDoc comment is made up of two parts, the description followed by block tags. 
Keep in mind that Javadoc is often read in it's source form, so it should be easy to read and understand without the generated web frontend.

First Sentence
--------------
Write the first sentence as a short summary of the method, 
as Javadoc automatically places it in the method summary table (and index). 
This first sentence, typically ended by a dot, is used in the next-level higher Javadoc. 
As such, it has the responsibility of summing up the method or class to readers scanning the class or package. 
To achieve this, the first sentence should be clear and punchy, and generally short.

While not required, it is recommended that the first sentence is a paragraph to itself.
This helps retain the punchiness for readers of the source code.

It is recommended to use the third person form at the start.
For example, "Gets the foo", "Sets the "bar" or "Consumes the baz".
Avoid the second person form, such as "Get the foo".

HTML Tags
---------
As a rule-of-thumb use the `standard format for doc comments <http://www.oracle.com/technetwork/java/javase/documentation/index-137868.html#format>`_ with plain HTML tags (no XHTML). 
For longer doc comments use :code:`<p>` to separate different paragraphs. 
Note that you are not allowed to use self-closing tags, e.g., :code:`</p>`. 
Place a single :code:`<p>` tag on the blank line between paragraphs:

.. code-block:: java

  /**
   * First paragraph.
   * <p>
   * Second paragraph.
   * May be on multiple lines.
   * <p>
   * Third paragraph.
   */
  public ...
  
Lists are useful in Javadoc when explaining a set of options, choices or issues. 
These standards place a single :code:`<li>` tag at the start of the line and no closing tag. 
In order to get correct paragraph formatting, extra paragraph tags are required:

Block Tags
----------

@code and @link
~~~~~~~~~~~~~~~
Many Javadoc descriptions reference other methods and classes. 
This can be achieved most effectively using the @link and @code features.

The @link feature creates a visible hyperlink in generated Javadoc to the target. 
The @link target is one of the following forms:

.. code-block:: java

  /**
   * First paragraph.
   * <p>
   * Link to a class named 'Foo': {@link Foo}.
   * Link to a method 'bar' on a class named 'Foo': {@link Foo#bar}.
   * Link to a method 'baz' on this class: {@link #baz}.
   * Link specifying text of the hyperlink after a space: {@link Foo the Foo class}.
   * Link to a method handling method overload {@link Foo#bar(String,int)}.
   */
  public ...
  
The @code feature provides a section of fixed-width font, ideal for references to methods and class names.
While @link references are checked by the Javadoc compiler, @code references are not.

Only use @link on the first reference to a specific class or method. 
Use @code for subsequent references. 
This avoids excessive hyperlinks cluttering up the Javadoc.

Do not use @link in the punch line. 
The first sentence is used in the higher level Javadoc. 
Adding a hyperlink in that first sentence makes the higher level documentation more confusing. 
Always use @code in the first sentence if necessary. @link can be used from the second sentence/paragraph onwards.

Do not use @code for null, true or false. The concepts of null, true and false are very common in Javadoc. 
Adding @code for every occurrence is a burden to both the reader and writer of the Javadoc and adds no real value.


@param, @return, and @throws
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Almost all methods take in a parameter, return a result or both. 
The @param and @return features specify those inputs and outputs. 
The @throws feature specifies the thrown exceptions. 
The @param entries should be specified in the same order as the parameters. 
The @return should be after the @param entries, followed by @throws.

Use @param for generics. If a class or method has generic type parameters, then these should be documented. 
The correct approach is an @param tag with the parameter name of where T is the type parameter name.

Use one blank line before @param. 
There should be one blank line between the Javadoc text and the first @param or @return. 
This aids readability in source code.

The @param and @return should be treated as phrases rather than complete sentences. 
They should start with a lower case letter, typically using the word "the". 
They should not end with a dot. This aids readability in source code and when generated.

Treat @throws as an if clause. 
The @throws feature should normally be followed by "if" and the rest of the phrase describing the condition. 
For example, "@throws if the file could not be found". This aids readability in source code and when generated.

@author
~~~~~~~
By convention we avoid the @author tag. It'll generally go out of date, and can promote code ownership by an individual. 
The version control system is in a much better position to record authors.

What to Document
----------------
As the documentation is intended to be used by other developers, it is important to document *what* a piece of code does.
Everyone can read the code and understand *how* it works but it should not be necessary to read 5-15 lines only to understand the basic usage of a method.
Therefore, everything which is not intuitive by the name of the method and parameters should be documented.

Public and Protected
~~~~~~~~~~~~~~~~~~~~
All public and protected methods should be fully defined with Javadoc. 
Especially complex methods, procedures with side-effects, and non-trivial operations should be documented well. 
Package and private methods do not have to be, but may benefit from it.
Trivial getters and setters can be omitted.

null-tolerance, Pre- and Postconditions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Whether a method accepts null on input, or can return null is critical information for building large systems. 
All non-primitive methods should define their null-tolerance in the @param or @return. Some standard forms expressing this should be used wherever possible:

- "not null" means that null is not accepted and passing in null will probably throw an exception, typically NullPointerException.
- "may be null" means that null may be passed in. In general the behaviour of the passed in null should be defined.
- "null treated as xxx" means that a null input is equivalent to the specified value.
- "null returns xxx" means that a null input always returns the specified value.

When defined in this way, there should not be an @throws for NullPointerException.

.. code-block:: java

  /**
   * Javadoc text.
   * 
   * @param foo  the foo parameter, not null
   * @param bar  the bar parameter, null returns null
   * @return the baz content, null if not processed
   */
  public String process(String foo, String bar) {...}

While it may be tempting to define null-handling behavior in a single central location, 
such as the class or package Javadoc, this is far less useful for developers. 
The Javadoc at the method level appears in IDEs during normal coding, 
whereas class or package level Javadoc requires a separate "search and learn" step.

Other simple constraints may be added as well if applicable, for example "not empty, not null". 
Primitive values might specify their bounds, for example "from 1 to 5", or "not negative".

Generate HTML JavaDoc
---------------------
To generate the JavaDoc HTML-pages for the project simply execute :code:`gradle javadoc` at the root of the project. 
The actual :code:`build.gradle` doesn't need to have any related scripting in it, the Javadoc Gradle plugin does it all!

The rendered HTML for the engine project will be contained in :code:`engine/build/docs/javadoc` and respective :code:`modules/<module>/build/docs/javadoc` for modules..