Translation
===========

Adding new languages to the game or helping out with translating single strings is easy and helpful 
as it allows players from all over the world to enjoy the game, unhindered by language barriers!

Internationalization / i18n
---------------------------
Internationalization (i18n) is the process to design software for different languages, without changing the code for each language.

The general process is easily explained with an example:

.. code-block:: java

   @RegisterSystem
   public class GreeterSystem extends BaseComponentSystem {
   
       private static final Logger logger = LoggerFactory.getLogger(GreeterSystem.class);
   
       @ReceiveEvent
       public void onPlayerSpawn(OnPlayerSpawnedEvent event, EntityRef player) {
           logger.info("Hello, new player.");
       }
   }

This system will print :code:`"Hello new player."`, every time a player spawns. 
However a german player would expect something like :code:`Hallo neuer Spieler.`
and a french :code:`Bonjour nouveau joueur.`.

Instead of using hardcoded strings, the idea is to use a key for the string and lookup the actual content depending on the player's language.
This logic is contained in the :java:ref:`TranslationSystem <org.terasology.i18n.TranslationSystem>`.



.. code-block:: java

   @RegisterSystem
   public class GreeterSystem extends BaseComponentSystem {
   
       private static final Logger logger = LoggerFactory.getLogger(GreeterSystem.class);
   
       @In
       private TranslationSystem translationSystem;
   
       @ReceiveEvent
       public void onPlayerSpawn(OnPlayerSpawnedEvent event, EntityRef player) {
           logger.info(translationSystem.translate("${MyModule:greeter#greet}"));
       }
   }

The parameter :code:`"${MyModule:greeter#greet}"` tells the translation system to search for an translation entry in the module :code:`MyModule` (use :code:`engine` for the engine project).
The entry is expected to be in a file named :code:`greeter.lang` containing the key :code:`greet`.

All i18n entries are registered in an asset file, located at :code:`assets/i18n/*.lang`.

For our example, we need a file :code:`MyModule/assets/i18n/greeter.lang`:

.. code-block:: json

  {
    "greet": "greet"
  }

This file contains a number of comma-separated entries with the key of the translation string. Values should be similar to the keys in this file.

Languages are than added in additional files with an :code:`*_xx.lang` prefix, where :code:`xx` should be an `ISO 639-1 <http://en.wikipedia.org/wiki/ISO_639-1>`_ two-letter language code.

For our example, we need :code:`MyModule/assets/i18n/greeter_en.lang`:

.. code-block:: json

  {
    "greet": "Hello new player."
  }
  
and similar to this one, :code:`MyModule/assets/i18n/greeter_de.lang`:

.. code-block:: json

  {
    "greet": "Hallo neuer Spieler."
  }

In these files the keys map to the entries in the general file, with the values being the translated strings.
It is not required to translate all these files by hand inside the json syntax. 
Instead, Terasology offers a weblate frontend, which is described in the next section.

Localization / l10n
-------------------
Localization (l10n) is the actual translation of the extracted strings and requires no or less programming effort.

There are currently two ways of translating the game:

1. **(Recommended)** Using our `Weblate <http://weblate.org/>`_ interface, available at http://translate.terasology.org/.
2. Manually creating or editing text bundle files.

The former is the better option, as it allows us to easily review new translations or suggested changes.

Using Weblate
~~~~~~~~~~~~~

To start off, log in to translate.terasology.org. 
The preferable login method is using your GitHub account - by doing so, 
your changes and translations will be recognized correctly in the Git commits.

All translations needed for Terasology can be found in the corresponding Weblate project - `Weblate/Terasology <http://translate.terasology.org/projects/terasology/>`_. 
The project contains a single subproject: Menu, where all of the strings, labels and error messages for the game's main menu can be translated. This sub-project is found under `Weblate/Terasology/Menu <http://translate.terasology.org/projects/terasology/menu/>`_.

If your language doesn't exist in the round-up yet, 
you can request the addition of it using the "New translation" panel in the Menu sub-project. 
Otherwise, pick an existing language and translate away! 
Note that since English is the launcher's default language, English strings can only be modified using :ref:`manual translation <manual_translation>`.

For more information on how to use Weblate, see the official `Translator guide <http://weblate.readthedocs.org/en/weblate-2.5/user/translating.html>`_ for Weblate 2.5.

.. _manual_translation:

Manual Translation
~~~~~~~~~~~~~~~~~~

First off, to keep things nice and clean, we advise you to work on the translation using a **feature branch**:

- :code:`git checkout develop`
- :code:`git branch feature/myTranslation`
- :code:`git checkout feature/myTranslation`

To create a new language file, copy the :code:`*.lang` file which you want to translate 
to a new file called :code:`*_xx.lang` in the :code:`assets/i18n` directory. 
As mentioned above, :code:`xx` should be an `ISO 639-1 <http://en.wikipedia.org/wiki/ISO_639-1>`_ 
two-letter code for your language. Next up, translate everything in menu_xx.lang to your target language! 
Every now and then, check up on your in-progress translation - the game's language can be changed in the *Settings - Player* menu. 
Some possible issues that may occur are long strings breaking UI elements and special characters not being rendered properly.

When your translation is finished, add a tiny flag to represent the language in the settings! 
To do this, download an appropriate 16x11 icon from the famfamfam.com icon pack (or create your own 16x11 icon) 
and place it inside :code:`engine/src/main/resources/assets/textures/ui/icons`. 
Rename it to :code:`flag_xx.png`, :code:`xx` being the two-letter code you've used before.

To submit the new translation,

- :code:`git commit <message etc.>`
- :code:`git push`
- :ref:`Open a new pull request <create_pr>`.