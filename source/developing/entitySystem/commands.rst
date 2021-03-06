Commands
========

This is an article for developers who want to use and create their own console commands (for example for mods).

Adding new console commands to Terasology is easy. The steps below show what is needed for console commands.
Command implementation

Command structure
-----------------

Every command must be implemented as a public method of a :java:ref:`ComponentSystem <org.terasology.entitySystem.system.ComponentSystem>`. **E.g.** the following command just displays "hello world" in the console.

.. code-block:: java

    @RegisterSystem
    public class MyCommands extends BaseComponentSystem {

        @Command( shortDescription = "Say hello", helpText = "Writes hello world to the console" )
        public String hello() {
            return "hello world";
        }

    }

Looking at this simple examples we can see several important things:

* The command method must be located in a class implementing :java:ref:`ComponentSystem <org.terasology.entitySystem.system.ComponentSystem>`
* The command annotation :java:ref:`@Command<org.terasology.logic.console.commandSystem.annotations.Command>` is necessary for every command
* One can specify a short description and a (probably) longer help text
* A returned string will be shown in the console.

Annotation and Command Name
---------------------------

To specify a new console command, just an **annotated public method** is needed in a :java:ref:`ComponentSystem <org.terasology.entitySystem.system.ComponentSystem>`. The annotation is

.. code-block:: java

  @Command

and marks the method as a command. The command will have the same name as the method,
**e.g.** if you name you method ``public void hello()`` the command ``hello`` will be available in the game.

Short Descriptions and Help Text
--------------------------------
Short descriptions and help texts can be added via the method annotation. To specify a short description, just add ``shortDescription = "text for short description"`` to the annotation, **e.g.**

.. code-block:: java

  @Command( shortDescription = "some command description" )

Probably longer help text can be specified via ``helpText`` in the annotaion. An example is given below:

.. code-block:: java

    @Command( helpText = "A command without short description, but with a longer help text." )

Displaying Text
---------------

Any value returned from the command (``String`` or ``Object``) will be displayed in the in game :doc:`console </playing/console>`.

You can also write directly to the console via the :java:ref:`Console <org.terasology.logic.console.Console>` class.

Parameters
----------

Of course it is possible to give parameters/arguments to your command when executed in the command line. These
arguments are specified as method arguments. It is highly recommended to prefix the method arguments by a parameter
annotation, that is used for the command line help.

.. code-block:: java

    @Command( shortDescription = "Echo-cho-cho-o-o", helpText = "Echoes the input text." )
    public String echo(@CommandParam( value = "Message" ) String message){
        return message;
    }

The method above will add an ``echo <string>`` command that simply echoes the input text. The command is proper annotated,
resulting in user friendly help messages and command description.

.. note::

  The supported types for command parameters are: ``float``, ``int``, ``String``. The ``final EntityRef`` parameter is supported only when the commands are set to ``runOnServer``. See :ref:`Commands and Multiplayer <commands_multiplayer>`

Commands and Multiplayer
------------------------

By default, commands run locally - on the client side.
A command can be marked as ``runOnServer``, in which case it will be replicated to the server in a multiplayer game and executed there:

.. code-block:: java

  @Command(runOnServer = true)

.. _commands_multiplayer:

.. note::

  In such a case, the command method can have a ``final EntityRef`` parameter. This will be populated with the Client entity of the calling player.

  .. code-block:: java

    @Command(shortDescription = "Sends a message to all other players", runOnServer = true)
    public void say(@CommandParam("message") String message, EntityRef speaker) {
    }
