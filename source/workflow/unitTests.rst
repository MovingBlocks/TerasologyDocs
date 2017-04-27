Unit Testing
============

Why Tests?
----------
Most developers spend the majority of their time not writing code, but debugging and maintaining it. 
Unit tests are one of the best ways to minimize unnecessary time spent on both. 
Testing also helps document your code. 
Finally, we use a passing unit test suite as one of the criteria for accepting pull requests.

Testing Libraries
-----------------
Terasology uses JUnit 4 for its automated test suite. 
It also uses Mockito for mocking/stubbing in special situations 
for which a dependency is too expensive or unreliable to bring into a test suite - for example, network activity or OpenGL.

An IDE is highly encouraged for running tests, as most support JUnit. 
In Eclipse, for example, you can quickly run a single test by right-clicking on the test method declaration 
and selecting Run As → JUnit Test. You can give this command a shortcut key of your choice to make it even faster.

Guidelines for Tests
--------------------

#. Ideally every line of code is backed up by a unit test. There are exceptions like straightforward getters/setters.
#. Run the full test suite when pulling changes and before making a pull request.
#. In the best case, start by `writing your tests first <http://en.wikipedia.org/wiki/Test-driven_development>`_.
#. Don't overuse mocks, stubs and spy objects. If you find yourself using Mockito a lot, consider to refactor the code to be more modular.
#. Tests for modules should be in the same project at :code:`src/test/java`. 
   Tests for the engine live in a separate project and are located at :code:`engine-tests/src/test/java`.

JUnit supports nested test classes. Our convention is to use a single outer class to test all of the functionality of a given class. 
Each inner class contains all tests for a single method on the object under test.

Example:

.. code-block:: java

   @RunWith(Enclosed.class)
   public class StringTest {
       public static class Equals {
           private String string;
           
           @Before
           public void setUp() {
               string = "Testing";
           }
   
           @Test
           public void testEqualStrings() {
               assertTrue(string.equals(testing));
           }
       }
   
       public static class IndexOf {
           private String string;
   
           @Before
           public void setUp() {
               string = "Testing";
           }
   
           @Test
           public void testIndexNotFound() {
               assertEquals(-1, string.indexOf("foobar"));
           }
       }
   }
   
Game Environment Tests
----------------------
Test classes that require a Terasology environment should extend :java:ref:`TerasologyTestingEnvironment <org.terasology.TerasologyTestingEnvironment>`, 
a test class that sets up a headless environment by initializing core game systems and providing access to them via the context field or the CoreRegistry.