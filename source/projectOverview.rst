Project Overview
================

.. _codebase_structure:

Codebase-Structure
------------------

.. todo::
   https://github.com/MovingBlocks/Terasology/wiki/Codebase-Structure

Sites
-----
Terasology is covered by mutliple online presences:

- `Community Portal and Forum <http://forum.terasology.org/>`_ - main site for announcements and discussion.
- :doc:`#terasology at Freenode IRC  </developerIntro/usingIrc>` - live chat and support when somebody is available (be patient!).
- `Meta Server <http://meta.terasology.org/>`_ - shows a list of game servers, modules, and so on. Can be used via API and is used as such by the game and launcher.
- The `Splash Site <http://terasology.org/>`_ - a small GitHub Page to intro the game, play via applet, or even run the soundtrack (top left - Flash).
- Social Networks: `Reddit <https://www.reddit.com/r/Terasology>`_ | `Facebook <https://www.facebook.com/Terasology>`_ | `Twitter <https://twitter.com/Terasology>`_ | `YouTube <https://www.youtube.com/user/blockmaniaTV>`_ | `G+ <https://plus.google.com/b/103835217961917018533/103835217961917018533/posts>`_.

GitHub Organizations
--------------------
The projects sources are organized in two `GitHub <https://github.com/>`_ organizations.
Central components of the project live under the `MovingBlocks <https://github.com/MovingBlocks>`_ organization.
It's main contents are:

- The `Engine <https://github.com/MovingBlocks/Terasology>`_, which is the heart of the game. It includes the PC Facade (the standard application) and the Core module with some basic gameplay elements - this is all you need to run the game.
- The `Launcher <https://github.com/MovingBlocks/TerasologyLauncher>`_, is the best way to run the game. It allows easy updating and maintaining different versions of the game.
- The `Splash Site Sources <https://github.com/MovingBlocks/movingblocks.github.com>`_, of http://terasology.org/.
- `TeraBullet <https://github.com/MovingBlocks/TeraBullet>`_ offers some voxel-world integrations with `JBullet <http://jbullet.advel.cz/>`_.
- `Tera OVR <https://github.com/MovingBlocks/TeraOVR>`_, a wrapper for the `Oculus Rift <http://www.oculusvr.com/>`_ SDK.
- `Gooey <https://github.com/MovingBlocks/Gooey>`_, our handy little `Hubot <http://hubot.github.com/>`_-based IRC bot offering witty banter and useful functionality like auto-creating GitHub repos. When he feels like it, anyway!
- The `gestalt <https://github.com/MovingBlocks/gestalt>`_ library bundle, which contains the logic for our :doc:`Asset System <concepts/assetSystem>`, :doc:`Module System <concepts/modules>` and :doc:`Entity System <concepts/entitySystem>`
- And some more, like our `repository configuration <https://github.com/MovingBlocks/TeraConfig>`_, `math libraries <https://github.com/MovingBlocks/TeraMath>`_, a `crash reporter <https://github.com/MovingBlocks/CrashReporter>`_, or `miscellaneous stuff <https://github.com/MovingBlocks/TeraMisc>`_.

Content modules and extensions to the actual game are bundled at the `Terasology <https://github.com/terasology>`_ organization.
It contains a large set of different modules which may extend the gameplay or provide further functions to other modules.
A small (and by far not complete) list of examples:

- `NeoTTA <https://github.com/Terasology/NeoTTA>`_, an experimental gameplay module with various features.
- `JoshariasSurvival <https://github.com/Terasology/JoshariasSurvival>`_, a gameplay module which bundles different modules with the focus on surviving and advancing technology.
- `LightAndShadow <https://github.com/Terasology/LightAndShadow>`_, an experimental game type in an Alice in Wonderland inspired setting.
- `MasterOfOreon <https://github.com/Terasology/MasterOfOreon>`_, a manager interface for minions.
- `DynamicCities <https://github.com/Terasology/DynamicCities>`_, city generation and population simulation.
- ...

External Projects
-----------------
Some noteworthy external projects which are used in Terasology:

- `LWJGL <http://lwjgl.org/>`_, as foundation for graphics, sound, and input.
- `Gradle-Git <https://github.com/ajoberstar/gradle-git>`_, which makes Gradle even more magical by adding Git tasks.
- `Jenkins CI <http://jenkins-ci.org/>`_, for continuous integration. Builds our stuff at http://jenkins.movingblocks.net.
- `Artifactory <http://www.jfrog.com/home/v_artifactory_opensource_overview>`_, repository manager, holds our builds and assorted library files, at http://artifactory.movingblocks.net.
- `XenForo <http://xenforo.com/>`_ - our portal/forum site at http://forum.movingblocks.net.



History and more
----------------
If you are interested in the project's history, the goals and the origin of the name, have a look at `What is Terasology`__.

__ https://github.com/MovingBlocks/Terasology/wiki/What-is-Terasology
