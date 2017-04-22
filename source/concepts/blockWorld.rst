Block World
===========

The most basic concept of Terasology is the block world.
The entire world is made up of blocks, each with one x-y-z-coordinate and a side-length of 1 unit.

Blocks are organized in chunks, which contain a larger area of blocks. In Terasology, each chunk has a size of 32x32 blocks and a height of 64 blocks. [#]_
A chunk has it's own x-y-z coordinates, similar to a block but in a larger space.

The world size is not hard-limited by the engine. Instead the maximum height/width/depth of a world is restricted by the coordinate value ranges (Java integer values) or memory/disk limitations to store the world.

Blocks have a limited number of :ref:`attributes <block_attributes>`. This makes them an efficient data format for storage on disk or serialization over the network.
If additional properties or behavior for blocks are required (e.g. a chest which has it's own inventory), then blocks can be :ref:`backed up to entities <block_entities>` (see the :ref:`Entity System <entity_System>` for details).

Have a look at the :ref:`blocks developer guides <blocks>` for further topics like the :ref:`block attributes <block_attributes>`, :ref:`shapes <block_shapes>`, or :ref:`entity-based properties <block_entities>`.

.. [#] Chunk size definition is contained in :java:ref:`ChunkConstants <org.terasology.world.chunks.ChunkConstants>`.
