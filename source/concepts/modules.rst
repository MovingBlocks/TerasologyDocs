.. _concept_modules:

Modules
=======

Modules are extensions/modifications to the engine. A Terasology module is a java project on it's own, which is resolved similar to a library an lives in it's own sandboxed environment.
The module system is implemented the `gestalt module <https://github.com/MovingBlocks/gestalt>`_ library.

Structure of Modules
--------------------

- :code:`/src` - actual source code for custom functionality goes here. Usually this will be custom components and systems which extend the :ref:`entity_System`.
- :code:`/assets` - Resources related to the module can be placed here and will be located by the :ref:`asset_system`. Sub-categories for assets like prefabs or block definitions are structured in sub-directories.
- :code:`/deltas` and :code:`/overrides` - Modification directories for existing assets. These mechanics are described at `TutorialAssetSystem/Deltas-and-Overrides <https://github.com/Terasology/TutorialAssetSystem/wiki/Deltas-and-Overrides>`_.
- :code:`build.gradle` - internal build file, should not be edited.
- :code:`module.txt` - Configuration file for the module, similar to a maven :code:`pom.xml` or gradle build file. Have a look at the :ref:`module_txt` section for details.

.. _module_txt:

module.txt
----------

Definition file for a module, using JSON syntax.
The following properties are supported:

- :code:`id` - the internal identifier of the module.
- :code:`version` - the version of the module, versions are stored in the format :code:`MAJOR.minor.patch(-SNAPSHOT)` (see :ref:`versions` for details).
- :code:`author` - the author(s) of the module, could be any string. Default are single names or comma-separated lists.
- :code:`displayName` - the name of the module which is shown ingame to the user.
- :code:`description` - a textual description, what the module contains and how it affects the game.
- :code:`dependencies` - a list of *dependencies*, which are mappings to other modules with a given version. Each dependency has the following properties:

  - :code:`id` - The id of the dependent module.
  - :code:`minVersion` - The minimum version of the dependent module (inclusive).
  - :code:`maxVersion` - The maximum version of the dependent module (exclusive).
  - :code:`optional` - If the dependency is optional. A module with optional dependencies should work, even if the optional dependencies are not available when the user starts a game.
  - :code:`serverSideOnly` - A boolean, indicates if the module should only be available on the server and not on the client. Such modules are not downloaded by a client when he connects to a server.
  - :code:`isGameplay` - A boolean, indicates if the module should appear in the list of gameplay modules. Typically, such modules contain little logic or assets themselves but bundle other modules together.
  - :code:`defaultWorldGenerator` - The id of the default world generator [#]_ which should be activated with the module.


Have a look at the `NeoTTA/module.txt <https://raw.githubusercontent.com/Terasology/NeoTTA/master/module.txt>`_ or other modules in the `Terasology <https://github.com/Terasology>`_ organization as examples.

.. [#] See :java:ref:`@RegisterWorldGenerator <org.terasology.world.generator.RegisterWorldGenerator>` for details.

Namespace
---------

The common namespace for a module is :code:`org.terasology.<nameOfTheModule>.*`. It is recommended to name source packages accordingly, otherwise modules may not be built or loaded as expected. [#]_

.. [#] See `#2445 <https://github.com/MovingBlocks/Terasology/issues/2445>`_ for more details.

Guides
------

The :ref:`Modules Guide <developing_modules>` delivers further information about fetching and creating modules, dependencies and the sandbox environment.
