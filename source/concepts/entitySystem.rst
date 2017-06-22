.. _entity_System:

Entity System
=============

Terasology's Entity System is the core framework for game logic - most everything in the world is an entity. An entity system was chosen as it provides a lot of flexibility and support for extension [#]_ [#]_ [#]_, and can quite easily support in-game editors and simple mods without any code needing to be written.

The GUI and blocks are not handled as entities, although some blocks may have a related entity.


Entities and Components
-----------------------

The heart of the entity system is a simple data structure composed of Entities and Components. 
Each Entity is a unique object in the world - the player is an entity, a single enemy is an entity, a chest is also an entity (linked to a block). 
Entities don't have to be objects that are visible in the world either - they can be scoreboards, loot tables, a UI, and other gameplay related things.

An entity on its own isn't really anything, though. For an entity to be of use it needs to be given components. 
Each component is a feature that an entity can have: a Location component gives an entity a position in the world, a Mesh component gives it appearance, a RigidBody component along with a shape component gives it collision, and so forth. 
Each component also can have properties that can be set, that relate the the feature it provides - Location component has a position property, Mesh component has the mesh to display.

This structure provides flexibility and reuse when creating entities. 
You can add any of the existing components to make use of their features, and concentrate on creating new components for any features that don't presently exist - if any.

Component Systems
-----------------

In Terasology, a component is essentially just a request for an entity to be given a feature, and some data that feeds into how that feature works. 
A component itself does not contain any logic for a feature - instead that is left to the so called systems.

A system provides the actual logic behind a component or combination of components - it can process them each frame, or respond to events dealing with them. 
Multiple components being involved is common - rendering a mesh from a mesh component cannot be done without a location from a location component.

There are a number of advantages to the separation between data (in the Components) and logic (in the Systems):

- Allows modules to modify the behaviour of components. If a modder doesn't like the default behaviour of the Health component, they can replace the Health system with their own version - that will still work with all the existing entities with a Health component.
- Allows optimisation of the processing of multiple entities.

Events
------

Terasology also includes an event system built around the entity system. Events can be sent to entities, and systems can subscribe to be notified about specific events, when they are received by entities with a desired combination of components.

For instance, when an entity is hit by a sword a DamageEvent is sent to it. 
This event includes the amount of damage dealt - it could also include information on the type of damage, the source of the damage and so forth. 
The health system would subscribe to the damage event but only for entities with a health component. 
So if the hit entity has a health component then the health system would receive the event and can react to it by subtracting health - potentially sending another event if the entity's health reaches zero.

This provides two valuable features:

1. It provides a mechanism for an entity to react to an event based on the components it has. This means that someone can later on create their own component and system combination that reacts to Damage events differently.
2. Because an event can be received by multiple systems, it is possible for modders to intercept and modify or cancel an event to change behaviour. An armor component could be added that halves all damage, and set up to intercept the damage event - without having to change the health system at all.

.. note::
  Have a look at :ref:`Events <events>` for a guide how to develop and listen for events.

.. [#] http://www.richardlord.net/blog/what-is-an-entity-framework
.. [#] http://www.richardlord.net/blog/why-use-an-entity-framework
.. [#] http://t-machine.org/index.php/2007/09/03/entity-systems-are-the-future-of-mmog-development-part-1/
