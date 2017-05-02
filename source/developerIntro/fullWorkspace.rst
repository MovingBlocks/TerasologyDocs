Full Workspace Setup
====================

The engine repository at https://github.com/MovingBlocks/Terasology is the heart and central workspace of mostly everything Terasology.

To set up the workspace is a fairly easy process:

* Git clone or download a source zip from GitHub to some location on your computer
  * See GitHub or Google for various Git tutorials. In short you'd clone with ``git clone https://github.com/MovingBlocks/Terasology.git`` into a local workspace directory
* Run ``gradlew`` once in the root of the chosen directory via command prompt / terminal

.. note::

  In OSX, the command is ``./gradlew`` instand of ``gradlew``

That's it, really! You now should have a functioning game workspace.

Requirements
------------

Okay, you might want a little more than that. The only mandatory requirement is a Java 8 SDK which you either download from `Oracle <http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html>`_ or get via `OpenJDK <http://openjdk.java.net>`_.

.. note::

  Using OpenJDK has a slightly higher risk for encountering :ref:`Common Issues <common_issues>` - for instance the `Launcher <https://github.com/MovingBlocks/TerasologyLauncher>`_ requires JavaFX which isn't always bundled with OpenJDK.

Beyond that you might want an IDE and some IDE plugins, see :ref:`Setup in IntelliJ <ide_intellij>` or :ref:`Setup in Eclipse <ide_eclipse>`. Maybe even a tool like `YourKit <https://www.yourkit.com>`_ to help profile game performance. But everything else really is optional!

Most our automation and project setup happens through `Gradle <http://gradle.org>`_ which the ``gradlew`` script downloads a version of if needed. The initial ``gradlew`` execution will download all project dependencies (Maven style - downloading half the internet). Just give it a while. Read more on :ref:`Codebase Structure <codebase_structure>` if interested.


Run game from source
--------------------

As long as you have the code and Java 8 you can run the game from source simply with ``gradlew game``

Any problem encountered at this point is usually from Java not being configured right, such as having an older version as your default Java. See :ref:`Common Issues <common_issues>` for more.

.. note::

  If the game itself behaves funny or crashes see if the `normal release download <https://github.com/MovingBlocks/Terasology/releases>`_ works. If not check the **Minimum Requirements** [#]_ and make sure your graphics card driver is up to date.

  Ask in the `Support Forum <http://forum.terasology.org/forum/support.20>`_ if issues remain, or come join us on ``#terasology`` on Freenode IRC. See :ref:`Using IRC <using_irc>` and please be patient :-) IRC isn't necessarily instant communication and it may take a while to get a reply.

You can also run a headless server from source using ``gradlew server`` - just run it in a second command prompt / terminal as it'll not accept further input (other than ``CTRL-C`` to break the process)

.. _ide_intellij:

IntelliJ
--------

Running from command line is good and fine and some enjoy simply working in a plain text editor. For those preferring a full integrated development environment (IDE) we recommend `IntelliJ <https://www.jetbrains.com/idea/download>`_

We have a series of customizations that prepare run configurations, Git integration, and so on for the project, specifically for IntelliJ. Eclipse has fewer of these but is still entirely usable, as is NetBeans, but you'll need to figure out some details there yourself.

To prepare project files for IntelliJ simply run ``gradlew idea`` which as any ``gradlew`` also does the initial dependency fetch so you can go straight from source download to ``gradlew idea`` you don't need a separate plain ``gradlew`` step.

Open the resulting ``Terasology.ipr`` as an existing project in IntelliJ

.. warning ::

  Do **not** create a new project or attempt to import the project via Gradle. It is possible to get that working but it may miss customizations and cause confusion.

.. warning ::
  After openning ``Terasology.ipr``, IntelliJ will show: **Unlinked Gradle project?** **Don't** click on **Import Gradle project**


The opened project should leave you with a series of run configurations to execute the game (and server) in various formats. It'll hook up our license header as a template, configure code analytics, and so on.

Here is a video introducing downloading project from GitHub, runing the game from sources and openning the source with IntelliJ:

.. youtube:: https://www.youtube.com/watch?v=cCMQ5VaKnfw

|

.. _ide_eclipse:

Eclipse
-------

Eclipse can be used with Terasology just like IntelliJ, but needs a little more manual setup.

.. todo::

  We have a few more files at ``config/eclipse`` that could use some setup instructions and/or automated customization like for IntelliJ.

.. note::

  All of the settings described below can be applied to a specific Eclipse project or to an entire workspace.

  - To apply the settings on a per-project basis, right-click on a project in the **Package Explorer** and select **Properties**. (Alternatively, select the project and press Alt+Enter) After navigating to a relevant section of the Preferences menu, check **Enable project-specific settings**. Repeat this for all the projects you'd like to work on.

  - To apply the settings globally, select **Window → Preferences** from the main menu and navigate to a relevant section.

- Formatting Convention Setup: In **Java Code Style → Formatter**, click **Import** and import Terasology's formatting settings file (`Terasology/config/eclipse/formatting.xml <https://github.com/MovingBlocks/Terasology/blob/develop/config/eclipse/formatting.xml>`_). The **Terasology formatting conventions** profile should be automatically selected.

.. image:: img/EclipseFormatterSettings.png

- Import Order Setup: In **Java Code Style → Organize Imports**, click Import and import Terasology's import order file (`Terasology/config/eclipse/.importorder <https://github.com/MovingBlocks/Terasology/blob/develop/config/eclipse/.importorder>`_).

.. image:: img/EclipseImports1.png

- **Optional, but recommended**: Switch to **Window → Preferences → Editor → Save Actions**. Check **Perform the selected actions on save** and **Organize imports**.

.. image:: img/EclipseImports2.png

Here is a video introducing setting up Terasology with Eclipse:

.. youtube:: https://www.youtube.com/watch?v=WMqGx9f28uM

|

Git
---

Git will be enabled as source control, however going deeper into the details of using Git is outside the scope of this wiki. Please `see the excellent resources on GitHub for more <https://help.github.com/articles/good-resources-for-learning-git-and-github>`_ like their `bootcamp <https://help.github.com/categories/bootcamp>`_ series.


.. seealso::

  * :ref:`Module concept <concept_modules>` and :ref:`Developing modules <developing_modules>` - if the engine is the heart of Terasology modules make up everything else. Learn about them here.
  * :ref:`Contributing <contributing>` - understand how to work on the GitHub (fork code repositories on GitHub,interact with several at once, etc).

.. [#] TODO: https://github.com/MovingBlocks/Terasology/issues/1123
