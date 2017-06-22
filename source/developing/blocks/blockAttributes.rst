.. _block_attributes:

Block Attributes
================

Block attributes are used in :code:`.block` files, as described in :ref:`Block Definition <block_definition>`.


Inheritance
-----------

Block definitions can extend from other block definitions, specifying just the features by which they differ.
This simplifies creating classes of block (like plants).

+----------+--------------------------------------------------+---------------+-----------------------------------------------------------------------+
| Option   | Value(s)                                         | Default       | Description                                                           |
+==========+==================================================+===============+=======================================================================+
| basedOn  | A block definition uri like :code:`engine:plant` |               | Specifies the block to base this block on.                            |
+----------+--------------------------------------------------+---------------+-----------------------------------------------------------------------+
| template | :code:`true`, :code:`false`                      | :code:`false` | If true, this block cannot be created and exists only to be based on. |
+----------+--------------------------------------------------+---------------+-----------------------------------------------------------------------+


Informational
-------------

+-------------+----------+---------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| Option      | Value(s) | Default                                                       | Description                                                                                                       |
+=============+==========+===============================================================+===================================================================================================================+
| displayName |          | The file name of the block, with the first letter capitalised | The name of the block that is shown to players - particularly when the block is picked up and in their inventory. |
+-------------+----------+---------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+


Core behavioural
----------------

+--------------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Option             | Value(s)                    | Default       | Description                                                                                                                                                                                          |
+====================+=============================+===============+======================================================================================================================================================================================================+
| attachmentAllowed  | :code:`true`, :code:`false` | :code:`true`  | Determines whether other blocks can be attached to this block.                                                                                                                                       |
+--------------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| hardness           | :code:`<int>`               | 3             | Specifies the hardness of the block - effectively its health.                                                                                                                                        |
+--------------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| liquid             | :code:`true`, :code:`false` | :code:`false` | Determines if the block is liquid.                                                                                                                                                                   |
+--------------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| replacementAllowed | :code:`true`, :code:`false` | :code:`false` | Specifies whether the block can be replaced freely by other blocks - that you can place another block over it. **In order to make a block replaceable, it requires the block not to be targetable!** |
+--------------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| supportRequired    | :code:`true`, :code:`false` | :code:`false` | Specify whether the block should be destroyed when no longer attached to any other block. **Only works for vertically adjacent blocks - e.g. grass is removed if the ground under it is destroyed**  |
+--------------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+


Tiles
-----

Tiles define the appearance of a block. They can be defined as :code:`tile` (one global texture for all sides of the block)
or :code:`tiles` (separate definition for different sides of the block).

+--------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| Option | Value(s)                       | Default                                                                                                                                                                                     | Description                                                               |
+========+================================+=============================================================================================================================================================================================+===========================================================================+
| tile   | A tile uri                     | By default, a block will try to use a tile texture with a matching filename. For example, the block for :code:`Grass.block` will use the block tile :code:`Grass.png` from the same module. | Specifies what tile to use to texture this block.                         |
+--------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
| tiles  | A list of tiles for each side. |                                                                                                                                                                                             | Alternative to the :code:`tile` property for blocks with different sides. |
+--------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+

The definition of :code:`tile` is straightforward. One example for the more complicated :code:`tiles` attribute:

.. code-block:: none

   "tiles" : {
    "sides"     : "core:ChestSides",
    "front"     : "core:ChestFront",
    "topBottom" : "core:ChestTopBottom"
   }

Valid block parts for :code:`tiles` are:

- **all** to change every tile. This has the same effect as using :code:`tile`.
- **topBottom** to change the top and bottom tile.
- **sides** to change the four horizontal sides (excluding top and bottom) and can itself be overridden.
- **front, left, right, back, top, bottom, center** refer to the specific side.

All these mappings refer to parts of a block shape. 
Have a look at :ref:`Block Shape Basics <block_shape_basics>` for a full overview over all parts.


Rendering Options
-----------------

+---------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Option        | Value(s)                    | Default       | Description                                                                                                                                                                                                                                                                        |
+===============+=============================+===============+====================================================================================================================================================================================================================================================================================+
| doubleSided   | :code:`true`, :code:`false` | :code:`false` | Whether this block should be rendered double sided. This done for billboard plants to render both sides of polygons.                                                                                                                                                               |
+---------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| invisible     | :code:`true`, :code:`false` | :code:`false` | If set to :code:`true` the block is excluded from rendering.                                                                                                                                                                                                                       |
+---------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| translucent   | :code:`true`, :code:`false` | :code:`false` | Determine whether the block is translucent or not. Blocks with this option enabled can use textures with transparency. Moreover, translucent blocks do not prevent occluded blocks behind them from beeing rendered (blocks behind a translucent glass block are still displayed). |
+---------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| shadowCasting | :code:`true`, :code:`false` | :code:`true`  | Determines if the block may cast shadows around it.                                                                                                                                                                                                                                |
+---------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| waving        | :code:`true`, :code:`false` | :code:`false` | Whether the block waves in the wind. May be used for grass or leaves.                                                                                                                                                                                                              |
+---------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| luminance     | :code:`<int>`               | 0             | The light level of the block. The default torches have a light value of 15, for reference.                                                                                                                                                                                         |
+---------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+


Color Lookup Tables
-------------------

Color gradients can be used to change the color of specific blocks, e.g. grass or fooliage.
This can be used for advanced block tinting, e.g. different grass colors in different biomes.

+--------------+---------------------------------------------------------------------------------------------------------------------+---------+---------------------------------------------------------------------------------------------------------------------------------------------+
| Option       | Value(s)                                                                                                            | Default | Description                                                                                                                                 |
+==============+=====================================================================================================================+=========+=============================================================================================================================================+
| colorSource  | One entry of :java:ref:`DefaultColorSource <org.terasology.world.block.DefaultColorSource>`, e.g. :code:`color_lut` |         | The color source to use.                                                                                                                    |
+--------------+---------------------------------------------------------------------------------------------------------------------+---------+---------------------------------------------------------------------------------------------------------------------------------------------+
| colorSources | Enumeration of color sources                                                                                        |         | Multiple color sources to use.                                                                                                              |
+--------------+---------------------------------------------------------------------------------------------------------------------+---------+---------------------------------------------------------------------------------------------------------------------------------------------+
| colorOffset  | :code:`[R, G, B, A]`                                                                                                |         | Specifies a color offset. For example for red leaves based on default leaves, one could use :code:`"colorOffset" : '[2.0, 0.0, 0.5, 1.0']`. |
+--------------+---------------------------------------------------------------------------------------------------------------------+---------+---------------------------------------------------------------------------------------------------------------------------------------------+

.. _shapes_and_rotation:

Shapes and Rotation
-------------------

Block shapes are specialised meshes that give a block its shape. If no shape is specialised then a block is a cube.

Generally for a non-cubic block you would define the shape with the shape property.


When using a block shape, it is often desirable to allow the block to rotate based on how it is being placed,
or even to have different shapes depending on how it is being placed. This can be enabled using the "rotation" property.
The following settings for :code:`rotation` are available:

- **none**, the block will not be rotated (default).
- **horizontal** for a block that will rotate on the horizontal place. For example, stairs will face towards the placer when placed.
- **alignToSurface** Similar to horizontal but with support for different blocks when placed against the ground or ceiling.

When using the alignToSurface rotation mode, you can specify a :code:`sides`, :code:`top` and/or :code:`bottom` section 
to provide override properties for those placements.

.. code-block:: none

   "rotation" : "alignToSurface",
   "sides" : {
       "shape" : "engine:stair",
   },
   "bottom": {
       "shape" : "engine:cube"
   }
   
This block would be shaped like a cube when placed on the ground, and shaped like stairs when placed against a side.
It cannot be placed against a ceiling (as no shape is defined for that case). Many properties can be overridden in this manner.

+--------------------+----------------------------------------------------------+---------------------+------------------------------------------------------------------------------------------------+
| Option             | Value(s)                                                 | Default             | Description                                                                                    |
+====================+==========================================================+=====================+================================================================================================+
| shape              | A shape uri                                              | :code:`engine:cube` | The shape of the block.                                                                        |
+--------------------+----------------------------------------------------------+---------------------+------------------------------------------------------------------------------------------------+
| shapes             | A list of shape uris                                     |                     | A list of valid shapes for this block.                                                         |
+--------------------+----------------------------------------------------------+---------------------+------------------------------------------------------------------------------------------------+
| rotation           | :code:`none`, :code:`horizontal`, :code:`alignToSurface` | :code:`none`        | The rotation mode for the block.                                                               |
+--------------------+----------------------------------------------------------+---------------------+------------------------------------------------------------------------------------------------+
| top, bottom, sides |                                                          |                     | In :code:`alignToSurface` rotation mode, this allows settings for specific surface placements. |
+--------------------+----------------------------------------------------------+---------------------+------------------------------------------------------------------------------------------------+

See :ref:`Block Shapes <block_shapes>` fore more information about the shape architecture.


Collisions
----------

+------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------+
| Option     | Value(s)                    | Default       | Description                                                                                                                  |
+============+=============================+===============+==============================================================================================================================+
| penetrable | :code:`true`, :code:`false` | :code:`false` | A block is penetrable if it does not block solid objects.                                                                    |
+------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------+
| targetable | :code:`true`, :code:`false` | :code:`true`  | Define whether the block can be targeted for interactions. **Must be set to** :code:`false` **to allow direct replacement.** |
+------------+-----------------------------+---------------+------------------------------------------------------------------------------------------------------------------------------+


Physics
-------

+-----------------+-----------------------------+--------------+--------------------------------------------------------------------------------------------------------------+
| Option          | Value(s)                    | Default      | Description                                                                                                  |
+=================+=============================+==============+==============================================================================================================+
| debrisOnDestroy | :code:`true`, :code:`false` | :code:`true` | If enabled destroyed blocks will drop a miniature instance of the block that can be picked up by the player. |
+-----------------+-----------------------------+--------------+--------------------------------------------------------------------------------------------------------------+
| mass            | :code:`<int>`               | 10           | The mass value for the physics simulation.                                                                   |
+-----------------+-----------------------------+--------------+--------------------------------------------------------------------------------------------------------------+

.. _block_entities:

Entity System Integration
-------------------------

As mentioned in :ref:`Block Definition <block_definition>`, blocks can be backed up by entites which are created from prefabs.
For example a chest block can link to the :code:`core:chest` prefab like so:

.. code-block:: none

   "entity" : {
       "prefab" : "core:chest"
   }

Inventory Settings
------------------

The inventory settings have to be in an inventory section as well. Taking the chest definition as example again:

.. code-block:: none

   "inventory" : {
       "stackable" : false,
       "directPickup" : true
   }

+--------------+-----------------------------+---------------+------------------------------------------------------------------------------------+
| Option       | Value(s)                    | Default       | Description                                                                        |
+==============+=============================+===============+====================================================================================+
| directPickup | :code:`true`, :code:`false` | :code:`false` | Whether this block should go directly into a character's inventory when harvested. |
+--------------+-----------------------------+---------------+------------------------------------------------------------------------------------+
| isStackable  | :code:`true`, :code:`false` | :code:`true`  | Determines whether the block type is stackable in the inventory.                   |
+--------------+-----------------------------+---------------+------------------------------------------------------------------------------------+


Categories
----------

Blocks may be marked with different categories, which can then be used by other systems.
For example, a shovel may be more efficient when digging in :code:`soil` blocks.
Categories are simple strings.

+------------+--------------------+---------+------------------------------------------------------------------------------------------------------------------------+
| Option     | Value(s)           | Default | Description                                                                                                            |
+============+====================+=========+========================================================================================================================+
| categories | list of categories |         | Give a list of categories the block belongs to. For example new soil types might use :code:`categories" : '["soil"']`. |
+------------+--------------------+---------+------------------------------------------------------------------------------------------------------------------------+
