.. _block_shapes_in_blender:
   
Block Shapes In Blender
=======================

Terasology has an easy-to-edit :ref:`shape format <block_shape_example>` for blocks. 
While the block shape format is hand editable and one could write a block shape by hand, 
there is a great addon for the free, open source 3d editor `Blender <https://www.blender.org/>`_
which allows to easily create block shapes in a visual WYSIWYG environment and export them for use in Terasology.

Block Shape Addon Installation
------------------------------

#. Download blender. Blender 2.60 was used when developing the addon so should be guaranteed to work. 
   Blender version 2.61 and 2.62 should also work, but anything newer (2.63 and up) will likely not.
#. Download the `TeraMisc <https://github.com/MovingBlocks/TeraMisc>`_. You can download the full source straight from github. 
   This is recommended, as it contains all the current shapes to inspect and all of the currently used textures. 
   As a last option, you could download the addon manually from https://github.com/MovingBlocks/TeraMisc/tree/master/blender_addons.
#. Install the Blender addon. In the TeraMisc project, you will find a directory called :code:`blender_addons`, 
   with a sub directory called :code`io_mesh_terasology`. 
   Copy this entire directory into :code:`[your blender install directory]/[your blender version]/scripts/addons` 
   (typically something like :code:`C:\Program Files\Blender Foundation\Blender\2.60\scripts\addons`).
#. Enable the addon in Blender. Start Blender, and open the user preferences page (under the File menu). 
   On the Addons tab find the **Import-Export: Terasology Block Shape Export** addon 
   (which you can easily do using the search bar on the left side of the window) 
   and activate it by checking the box on the right. 
   You will then want to save the user preferences so that the addon stays enabled after you close Blender and then restart. 
   Otherwise, you will have to re-enable the addon every time you start up Blender.

Fundamentals
------------
A block shape in blender is a set of mesh objects corresponding to the various parts of the block shape. 
For each side and the center part of the block shape, a mesh object with the corresponding name can be present: 
Top, Bottom, Left, Right, Front, Back and Center. 
Additionally, extra mesh objects can be used to define the collision bounds for the block shape.

When creating a block shape, you need to keep the following in mind:

- Blocks should be created centered on the origin.
- A standard block is half the scale of a new Blender cube.
- Blender axes are different from Terasology's axes, as shown in the following table:

+----------+----------------------+-------------------+
| Part     | Terasology Direction | Blender Direction |
+==========+======================+===================+
| Center   |                      |                   |
+----------+----------------------+-------------------+
| Right    | X+                   | X-                |
+----------+----------------------+-------------------+
| Left     | X-                   | X+                |
+----------+----------------------+-------------------+
| Top      | Y+                   | Z+                |
+----------+----------------------+-------------------+
| Bottom   | Y-                   | Z-                |
+----------+----------------------+-------------------+
| Back     | Z+                   | Y+                |
+----------+----------------------+-------------------+
| Front    | Z-                   | Y-                |
+----------+----------------------+-------------------+


Tips When Creating A Shape
--------------------------

- To avoid problems later in the creation process, scale in Edit Mode instead of Object Mode.
- When UV mapping, you should map against a single 16x16 texture.
- To preview your shapes texture after unwrapping, you can switch a 3d view in Blender to Textured shading. 
  Additionally, having mipmapping turned off will give a display very similar to what you will see in-game. To disable mipmapping:
  - Go to the user preferences (File menu).
  - In the user preferences window, go to the **System** tab.
  - In the middle near the top you should find a checked option that says **Mipmaps**. Uncheck this.


Terasology Exporter Addon Properties
------------------------------------

The Terasology Block Shape addon adds two panes to the 3d view properties side panel in Blender.

The first pane, Terasology Scene Properties, contains settings that are universal (not based on what mesh you have selected):

- Author - Your name here
- Collision Type
- Is Collision Symmetric - Is collection unchanged if the block is rotated?
  If checked, then definitions using this shape will not have a block generated for each rotation.
- Use Billboard Normals - For flat, vertical billboards, this causes the normals to point upwards so they are lit correctly by sunlight.

The second pane, Terasology Mesh Properties, contains settings that apply to the currently selected mesh object:

- Full Side - Does this side fill the block's space - this will cause the side of blocks facing it not to be rendered.
- Collider Type

Block Shape Video Tutorial
--------------------------

The process is also available as a video tutorial:

.. youtube:: https://www.youtube.com/watch?v=BM219wj0v6Y

.. youtube:: https://www.youtube.com/watch?v=cCApQJ5q6po