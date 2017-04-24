Documentation (External)
========================

Documentation for a larger scope than JavaDoc on single code elements exists at some additional places:

- Lots of the official documentation is contained in the `engine wiki <https://github.com/MovingBlocks/Terasology/wiki>`_.
  Larger parts of this documentation have been adopted from the original wiki pages.
- Some threads in the `forum <http://forum.terasology.org/forum/>`_ describe the ideas and architecture behind a special topic.
  It may require some digging but there is most likely an old thread with further information to a topic which is not part of this documentation.
- Some modules and libraries like the `gestalt library <https://github.com/MovingBlocks/gestalt/wiki>`_ contain their own documentation.
- Special topics are covered by tutorial modules which help to get started:

  1. `Asset System <https://github.com/Terasology/TutorialAssetSystem>`_ - introduction to assets, e.g. creating a block.
  2. `World Generation <https://github.com/Terasology/TutorialWorldGeneration>`_ - introduction to the faceted world generation.
  3. `NUI <https://github.com/Terasology/TutorialNui>`_ - introduction to NUI, the user interface which is used in the game.

  
  
Sphinx Documentation
--------------------

The documentation from this page is based on the `Sphinx <http://sphinx-doc.org/>`_ documentation generator.
All pages contain an "Edit on GitHub" link, which links back to the reStructuredText (rst) sources.

.. note::

   If you find pages missing, errors or outdated information, feel free to submit a pull request or open an issue at the repository.

The following section gives a short overview over the used syntax and some internal conventions.

Directory Structure
~~~~~~~~~~~~~~~~~~~
The sources are structured in own directories, relating to the sidebar navigation. 
Larger subtopics are structured in separate subfolders.
Each folder contains a :code:`.rst` file with the same name, containing the headline and a table of contents for the folder.
Images and other resources are located in a folder next to the file which uses the resource.



Headlines
~~~~~~~~~
Sphinx can handle nested tables of contents and documents.
Therefore each document can start with a main headline at the begin.

We use :code:`===` for headlines, :code:`---` for sections and :code:`~~~` for subsections.
If a deeper intendation is required, it could make sense to split the document and create a nested structure of smaller documents instead.

.. code-block:: rst

   Headline
   ========

   Section
   -------

   Subsection
   ~~~~~~~~~~

   
JavaDoc Links
~~~~~~~~~~~~~
We use `javasphinx <https://github.com/bronto/javasphinx>`_ with the engine javadoc included.
For better readability, the packages should be ommitted.

Example for the **class** :java:ref:`Event <org.terasology.entitySystem.event.Event>`:

.. code-block:: rst

   :java:ref:`Event <org.terasology.entitySystem.event.Event>`


Example for the **method** :java:meth:`EntityRef.send(Event) <org.terasology.entitySystem.entity.EntityRef.send(T)>`:

.. code-block:: rst
   
   :java:meth:`EntityRef.send(Event) <org.terasology.entitySystem.entity.EntityRef.send(T)>`
   
Example for the **constructor** :java:construct:`LocationComponent(Vector3f) <org.terasology.logic.location.LocationComponent.LocationComponent(org.terasology.math.geom.Vector3f)>`:

.. code-block:: rst

   :java:construct:`LocationComponent(Vector3f) <org.terasology.logic.location.LocationComponent.LocationComponent(org.terasology.math.geom.Vector3f)>`
   
External Links
~~~~~~~~~~~~~~

If a link fits in the text, the link can be included using the short syntax.

Example for a **link** to `the forum <http://forum.terasology.org/>`_:

.. code-block:: rst

   `the forum <http://forum.terasology.org/>`_
   
External notes or references can also be added as footnotes.

Example for a **footnote** to the forum [1]_:

.. [1] http://forum.terasology.org/

.. code-block:: rst

   the forum [1]_:

   .. [1] http://forum.terasology.org/

   
Code Snippets
~~~~~~~~~~~~~

Short inline code can be added via the :code:`:code:`<code>`` directive.

Longer snippets can be added as code blocks, like so:

.. code-block:: rst

   .. code-block:: java
   
      public static void main(String[] args){...}    

Which would result in the following code snippet:

.. code-block:: java
   
      public static void main(String[] args){...} 