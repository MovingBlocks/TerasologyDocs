Dependency Injection
====================

A :java:ref:`ComponentSystem <org.terasology.entitySystem.systems.ComponentSystem>` 
is not able to do much on its own except :ref:`sending an receiving events <events>`.
If it needs access to further logic, for example to modify blocks, has to use additional services from the engine.

Inject an Instance
------------------

The engine provides a mechanism for field injection to component systems. One example to obtain an instance of a
:java:ref:`BlockManager <org.terasology.world.block.BlockManager>` could look like this:

.. code-block:: java

  @RegisterSystem(RegisterMode.ALWAYS)
  public class MySystem extends BaseComponentSystem {
    
    @In
    private BlockManager blockManager;
  }
  
When a component system is created, all fields marked with the :java:ref:`@In <org.terasology.registry.In>` annotation will be injected.
The fields do not have to be public, it is even recommended to mark them as **private**.

.. warning::

  1. Injected fields are :code:`null` when the class is created, so don't access them in the constructor.
  2. Other systems may not be initialized before :java:ref:`ComponentSystem.initialise() <org.terasology.entitySystem.systems.ComponentSystem.initialise()>` is called.
     It is not guaranteed, that other systems are already initialized when they are accessed in the :code:`initialize()` method.

Share a Class
-------------

It is also possible to make own implementations available for dependency injection.
A system marked with the :java:ref:`@Share <org.terasology.registry.Share>` annotation is registered to be injected in other classes.

.. note::

  It is highly recommended to share an interface instead of the exact class.

One example to provide a new service:

.. code-block:: java

  public interface MyService {

      void doSomething();
  }
  
A component system implements this interface and is marked with the :code:`@Share` annotation, using the interface type as value:

.. code-block:: java

  @Share(MyService.class)
  @RegisterSystem(RegisterMode.ALWAYS)
  public class MyServiceSystem extends BaseComponentSystem implements MyService {

      @Override
      public void doSomething() {
          //...
      }

  }
  
When another system wants to access :code:`MyService`, it can add a field for it:

.. code-block:: java

  @In
  private MyService myService;
  
When the systems are initialized, this field will have the instance of our :code:`MyServiceSystem` as value.

How it works
------------

There are two systems to register classes for dependency injection.
The :java:ref:`CoreRegistry <org.terasology.registry.CoreRegistry>` is the older system and provides a static mapping from classes to instances, comparable to a singleton pattern.

The :java:ref:`Context <org.terasology.context.Context>` does pretty much the same in a non-static way and should be used for every new implementation in the dependency injection layer.

Logic for the actual dependency injection is available in the :java:ref:`InjectionHelper <org.terasology.registry.InjectionHelper>`.
It provides methods to inject fields in a class from a given context or the core registry.

.. note::

  Dependency injection is also available in other parts of Terasology than only component systems.
  Other examples may be NUI widgets, World Generators and some more.