.. _common_issues:

Common Issues
=============

Not everything succeeds on the first try. When that happens check this page to see if we've covered it. The main wiki pages try to be brief and avoid most troubleshooting.

If you encounter an issue not mentioned below try to check Google real quick, then consider asking in our `Support Forum <http://forum.terasology.org/forum/support.20>`_ or on ``#terasology`` on Freenode IRC. Please read :ref:`Using IRC <using_irc>` for more and be patient as it can take a while to get a reply :-)


Game
----

* The most common cause for game crashes is older video cards, **especially** Intel HD Graphics on laptops. Make sure you have the very latest graphics drivers available.
* If you're using a laptop that has a discrete NVIDIA GPU and Intel HD Graphics, the game may be attempting to run on the latter, causing a crash. To make the game use the discrete GPU,

  * Right-click on your desktop, select NVIDIA Control Panel. If the option doesn't show up, `install the latest NVIDIA drivers <http://www.geforce.com/drivers>`_.
  * Select *Manage 3D settings*.
  * Select *Program Settings*, then navigate to wherever the Terasology executive file is located and select it.
  * In the processor selection dropdown, choose **High-performance NVIDIA processor** and click Apply.
* You may run out of memory if your system doesn't have much available or you run the game with too little memory assigned and too high view distance. Especially with a 32-bit system or Java (has failed on even taking large screenshots in the past)

  * To run with increased memory you can launch via command prompt / terminal with something like: ``java -Xms128m -Xmx2048m -jar libs/Terasology.jar`` which will assign a max of 2 GB (but crash with a 32-bit Java! Can't assign more than around 1.5 GB)


IntelliJ
--------

* Be sure to open an existing project and use project files generated with ``gradlew idea`` - importing via Gradle or other options can leave you with broken project config at worst and missing a bunch of utility at least.
* For a first time install of IntelliJ you may not have a defined JDK available at a platform level. Look at **File -> Project Structure -> SDKs** and use the green + if needed to point to a local JDK 8. If not you may get errors about basic Java language features missing

  * After setting this up or if you name your JDK 8 something other than the default "1.8" you may have to set that to the Project SDK, again on the Project Structure page
* Any time you change the overall project structure by adding/deleting modules or pull updates from elsewhere that contain library changes you may have to run ``gradlew idea`` again to refresh your project config and get new dependencies.


Java
----

* It can be tricky to make sure the right version of Java is being used in different situations (within an IDE, via command line, on a server ..) - check the following options if needed:

  * System ``JAVA_HOME`` environment variable
  * System `PATH` environment variable
  * The ``update-alternatives`` or ``update-java-alternatives`` commands available on some Linux systems can override what's set via ``JAVA_HOME``. See `this Ask Ubuntu thread <http://askubuntu.com/questions/159575/how-do-i-make-java-default-to-a-manually-installed-jre-jdk>`_ or check Google.
* The Java installation picker (which download you get from https://www.java.com/en/download) may give you a 32-bit installer if you're using a 32-bit browser on a 64-bit system. Use 64-bit if you can!

  * Use ``java -version`` to find out what you have. This in turn may also depend on your OS. For instance, Windows may default a command prompt to ``C:\Windows\System32`` which will give you bad info. Try from ``C:\`` or anywhere else instead.
  * The 64-bit version explicitly states it is 64-bit (like ``64-Bit Server VM``) where 32-bit may call itself something like ``Client VM``
* If you do development and have something like Android Studio installed you may have had your system classpath modified. This can cause trouble if a system version of some Java dependency gets used in favor of a version we bundle.

  * Example: If you get an error like **Caused by: java.lang.UnsatisfiedLinkError: Can't obtain static method fromNative(Method, Object) from class com.sun.jna.Native** then try running the game with ``java -Djna.nosys=true -jar libs/Terasology.jar -homedir`` to ignore the system-provided version of JNA

Linux
-----

* Watch out for line-ending issues. For instance, the ``gradlew`` script might throw an error like **bash: ./gradlew: /bin/bash^M: bad interpreter: No such file or directory** if it somehow ends up with Windows-style line endings.
* If having issues with SSL when using ``gradlew``, run ``update-ca-certificates -f`` as root (or using ``sudo``).

Arch/Gentoo random problems
---------------------------

Both Arch and Gentoo do not include java jfx (needed for the launcher) by default when installing java.

On Arch you need to install the ``java-openjfx`` package, and on Gentoo you need to use the ``javafx`` USE flag when compiling java.


xrandr is a generic linux dependency for terasology, but the cases where you have it uninstalled usually only happen on arch and gentoo.
