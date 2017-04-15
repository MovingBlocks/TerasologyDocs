Asset System
============


Prefabs
-------
A prefab is a recipe for creating entities. Prefabs mimic the an actual entity - they have components with all the usual values - but are not processes by systems. Instead they can be used to create an entity with the same components and the same settings.

Additionally, prefabs can be used as a read-only source of information, without ever making entities from them. They could be used to describe crafting recipes for instance.

In Terasology, prefabs can be defined in a JSON format and included in modules.