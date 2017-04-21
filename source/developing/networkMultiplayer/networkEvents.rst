.. _entity_networking:

Entities, Components and Events on the Network
==============================================

.. todo::
   https://github.com/MovingBlocks/Terasology/wiki/Entities,-Components-and-Events-on-the-Network
   

.. _network_events:
   
Network Events
--------------
Events annotated with :code:`@ServerEvent`, are sent to the server. Only systems on the server will then be able to process it. Typically those events are requests to the server to confirm a gameplay related change. For that reason their name often ends with Request instead of Event.

Events annotated with :code:`@BroadcastEvent` are sent by the server to all clients.

.. todo::
   What happens if a client tries to send this event?

Events annotated with :code:`@OwnerEvent` are sent by the server to the client that owns the entity. Typically a client only owns its character and stuff related to it.

If a system on a client/server is responsible for processing an event, it can and should also be defined via a network filter which can be specified in the :code:`@RegisterSystem` annotation of the service or within :code:`@ReceiveEvent` annotation of the handling method.
