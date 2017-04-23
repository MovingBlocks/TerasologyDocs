Network Events
==============

.. _network_events:

By default, system events aren't sent over the network. To send events over the network, you should mark the event as :ref:`ServerEvent <networkEvents_serverEvent>`, :ref:`BroadcastEvent <networkEvents_broadcastEvent>` or :ref:`OwnerEvent <networkEvents_ownerEvent>`

.. note::
  If an event is marked as a network event, its fields are all replicated by default.

.. _networkEvents_serverEvent:

ServerEvent
-----------

Events annotated with :java:ref:`@ServerEvent <org.terasology.network.ServerEvent>`, are sent to the server. Only systems on the server will then be able to process it. Typically those events are requests to the server to confirm a gameplay related change. For that reason their name often ends with Request instead of Event.

When events marked with :java:ref:`@ServerEvent <org.terasology.network.ServerEvent>` are sent on the client, they will be replicated to the server as well so that they can be actioned there.

This is very important for events that require action on the part of the server, such as :java:ref:`AbstractMoveItemRequest <org.terasology.logic.inventory.events.AbstractMoveItemRequest>` and :java:ref:`DropItemRequest <org.terasology.logic.inventory.events.DropItemRequest>`.

.. code-block:: java

  @ServerEvent
  public abstract class AbstractMoveItemRequest implements Event {

.. code-block:: java

  @ServerEvent(lagCompensate = true)  
  public class DropItemRequest implements Event {

.. note::
  You can also specify the ``lagCompensate`` element when marking events with the `@ServerEvent` annotation, as seen from `DropItemEvent` It is false by default.  If set to true, however, the positioning of all characters on the server will be rewound to simulate the conditions on the client when the event was initially sent before the event is processed by the server.

  In the case of :java:ref:`DropItemRequest <org.terasology.logic.inventory.events.DropItemRequest>`, there is a need for ``lagCompensate`` to be set to true as the item should be dropped at the position where the character was when the request was initially sent, rather than the position where the character is when the event is received by the server. This thus takes into account the time taken for the request to be sent from the client to the server.

.. _networkEvents_broadcastEvent:

BroadcastEvent
--------------

Events annotated with :java:ref:`@BroadcastEvent <org.terasology.network.BroadcastEvent>` are sent by the server to all clients.

.. todo::
   What happens if a client tries to send this event?


.. _networkEvents_ownerEvent:

OwnerEvent
----------

Events annotated with :java:ref:`@OwnerEvent <org.terasology.network.OwnerEvent>` are sent by the server to the client that owns the entity. Typically a client only owns its character and stuff related to it.


.. note::
  If a system on a client/server is responsible for processing an event, it can and should also be defined via a network filter which can be specified in the :java:ref:`@RegisterSystem <org.terasology.entitySystem.systems.RegisterSystem>` annotation of the service or within :java:ref:`@ReceiveEvent <org.terasology.entitySystem.event.ReceiveEvent>` annotation of the handling method. See more detail about provessing an event in :ref:`Processing events <eventsSystems_processingEvents>`
