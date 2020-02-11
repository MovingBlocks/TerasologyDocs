.. _developing_modules:

Modules
=======

To work with modules you need to either fetch existing ones or create new ones. Terasology offers utility tasks in gradle to make this process easier.
We will use the :code:`Sample` module from https://github.com/Terasology/Sample for further examples.

Terasology's Git Setup
----------------------

Modules are structured as separate git repositories, nested in the engine repository.
The main project will contain the engine and everything else with modules located at the :code:`/modules/*` directory.

These nested git repositories are excluded from tracking in the engine git repo, holding the main Terasology project.
Therefore modules and the engine are treated independently in version control. The following diagram explains this concept:

.. image:: img/modulesGitConcept.png

Fetching existing Modules
-------------------------

Existing modules from the `Terasology organization <https://github.com/terasology>`_ can be fetched by running 

:code:`groovyw module get Sample` from the root of the Terasology workspace.

In this example, :code:`Sample` is the name of the module to fetch. Gradle will fetch the existing GitHub repository from https://github.com/Terasology/Sample to your workspace at :code:`modules/Sample`.

To properly adjust your workspace you need to regenerate the additional project files via :code:`gradlew idea`.

The main difference to a :code:`git clone` is, that the gradle command will include a :code:`build.gradle` to the module, along with placeholder directories for all asset types and such.
For modules which are not available under the Terasology organization, the repository has to be cloned and a :code:`build.gradle` from another module, e.g. from *Core* has to be copied into the cloned module.


.. note::
   Sometimes :code:`gradlew idea` does not add the module for you. To do this, simply activate the :code:`<moduleName>.iml` file and select :code:`Import <ModuleName> Module`.

Create a new Module
-------------------

New modules can be created with a similar command:

:code:`groovyw module create MySample`.

This will create a module named *MySample* at :code:`modules/MySample`.

Similar to fetching a module, be sure to adjust your workspace after your module lineup has changed. 
Running :code:`gradlew idea` from the root directory will create the required project files.

By default, the module will be initialized with an empty git repository.
Connecting the new module to GitHub can be done in one of two ways, either of which needs you to create a new remote reference in the local git repository.

1. You can create your own module repository on your personal GitHub account.
2. You can ask the project staff to please create a module repository for you under the `Terasology organization <https://github.com/terasology>`_ and give you access. This is also possible later on.

After you have a module repository on GitHub and still from :code:`modules/MySample`, execute :code:`git remote add origin <repository_url>`, where :code:`repository_url` is either your personal repository url or the official repository url.

.. note::
   Of course, you can have a private repository and a link to an official repository at the same time, e.g. with *origin* as name for your private repository and *terasology* as name for the official repository.
   It is up to you, how you finally organize your module setup.
   
Dependency Resolution
---------------------

You may end up fetching or creating a module that depends on other modules. Again our Gradle setup makes this super easy to handle!

If you fetch a module :code:`X` that has a dependency on module :code:`Y` the next execution of any :code:`gradlew` command will automatically fetch a binary copy (typically a :code:`.jar`-file) of module :code:`Y` including in turn any of its dependencies (a "transitive" dependency).

Any binary module dependency will be stored both in your local Gradle cache as well as in :code:`/modules` where the game will use it from at runtime.

If you later fetch the source code for module :code:`Y` it will automatically take precedence over any old binary copy of :code:`Y`.

You can delete any binary copies of modules at any time then rerun :code:`gradlew` to have them re-fetched.

Modding API & Sandboxing
------------------------

Terasology's engine uses a whitelisting approach to expose API for modules using two primary methods and a rarely needed third one:

1. Internal classes or packages marked with the :code:`@API` annotation are available to all modules.
2. External classes or packages in the basic whitelist at :code:`org.terasology.engine.module.ExternalApiWhitelist` are available to all modules.
3. Rarely blocks of code in the engine may be hit in a way requiring use of :code:`AccessController.doPrivileged(...)` - usually this is nothing module authors have to worry about but once in a while it could explain something quirky.

This API has two bearings: First, it aims to protect the user's system from malicious code (for instance the direct use of :code:`java.io.File` is not possible) and second, to better document what is available.
If one attempts to use a class which is not whitelisted in one of these cases, this will result in a log message like:

:code:`Denied access to class (not allowed with this module's permissions): some.package.and.class`.

While modules can themselves use the :code:`@API` annotation to mark interesting code for reuse no special security is attached at this point beyond the engine. Any module can use anything from any other module it declares as a dependency.

The :code:`org.terasology.documentation.ApiScraper` class will output a list of all :code:`@API` marked functionality. [#]_ [#]_ [#]_

For more information of how the module sandbox works, see the `Gestalt Module Sandboxing wiki page <https://github.com/MovingBlocks/gestalt/wiki/Module%20Sandboxing>`_, including how to disable security entirely for prototype work.

.. [#] `Sample output <https://github.com/MovingBlocks/Terasology/issues/1975#issuecomment-180944901>`_ of the :code:`ApiScraper` as of early Feb. 2016.
.. [#] More annotations like :code:`@Command` could be added to the API, `#2159 <https://github.com/MovingBlocks/Terasology/issues/2159>`_.
.. [#] Documentation is still in overhaul phase, `#1975 <https://github.com/MovingBlocks/Terasology/issues/1975>`_.