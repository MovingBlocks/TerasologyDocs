.. _block_definition:

Block Definition
================

Block data can be defined on four locations, all inside the :code:`assets` folder:


#. :code:`blocks` contains the block definitions. All files in this folder should have a :code:`.block` extension.
   Block definitions are limited to a number of properties. See :ref:`block_attributes` for a complete list.
   
#. :code:`blockTiles` contains the block tile textures. The textures should be in the :code:`.png` format with a size of :code:`16x16`.

#. :code:`shapes` contains special shapes for blocks with a unique model. Files in this folder should have a :code:`.shape` extension. 
   See :ref:`Block Shapes <block_shapes>` for a full reference on how to generate these files from blender.

#. :code:`prefabs` can be used to define extra behavior for blocks via :ref:`prefabs <prefabs>`.
   Files in this folder should have a :code:`.prefab` extension. Everything which can not be defined in the :code:`.block` file should be defined here. 
   In most of the cases, this will be Components and their initial values. 
   Think about a spike component on a cactus block, which defines how many damage you will take if you touch the block.