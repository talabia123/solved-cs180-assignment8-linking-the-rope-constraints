Download Link: https://assignmentchef.com/product/solved-cs180-assignment8-linking-the-rope-constraints
<br>
<h1>1.1        Linking the rope constraints</h1>

In rope.cpp, implement the constructor of the class Rope. It should create a new Rope object starting at start and ending at end, containing num nodes nodes. That is, something like the following diagram:

Each node is a <strong>mass</strong>, and each line between them is a <strong>spring</strong>. By creating a set of springs and masses, you create an object that behaves like a spring.

The nodes at the indices specified by <strong>pinned nodes </strong>should have their pinned attribute set to true (those will be stationary). For each node, you should create a Mass object, and set the mass and spring constant <strong>k </strong>into the Mass constructor (PLEASE check the code/header files to check what exactly you should pass to the constructor). You also should create a spring between consecutive masses, again check the signatures of the constructors to see what you should pass as arguments to it.

Run ./ropesim. You should see the rope drawn to the screen, although it won’t be moving for now.

<h1>1.2       Explicit/Implicit Euler</h1>

Hooke’s law states that the force on two points along a spring is proportional to their distance. That is,

In Rope::simulateEuler, first implement Hooke’s law. Iterate over all the springs and apply the correct spring force to the mass on either end of the spring. Ensure that the force is pointing in the correct direction! Accumulate all forces due to springs in the forces attribute of each Mass.

Once all the spring forces have been computed, apply the laws of physics to each particle:

Run ./ropesim. Your simulation should start running, but as it only has 3 nodes, it doesn’t look like much. At the top of application.cpp, you should see where the Euler and Verlet ropes are defined. Change the value 3 for the number of nodes to a higher constant like 16 for both ropes.

Run ./ropesim -s &lt;step-count&gt; to set the simulation to use a different number of simulation steps per frame. Try small values and large values (default is 64).

<h1>1.3      Explicit Verlet</h1>

Verlet is a different way of ensuring that all constraints are dealt with accurately. The benefit to this approach is that the simulation is handled entirely through the positions of the vertices in the simulation, and it remains fourth-order accurate! Unlike Euler, Verlet integration follows the following rule to calculate the next position in the simulation:

In addition, we can now emulate springs with an infinite spring constant. Instead of bothering with spring forces, we simply move each mass’s position such that the springs are set back to their rest length. The correction vector should be proportional to the displacement between the two masses and in the direction between one mass and the other. Each mass should move by half the displacement.

As long as we do this for every pair of springs, the simulation should approach stability. Additional rounds of simulations may be necessary to make the motion smoother.

<h1>1.4     Damping</h1>

Add damping to Hooke’s law in explicit Verlet. Springs in real life don’t continue bouncing forever – energy is lost to friction. Use damp factor 0.00005. The damping is applied by:

<h1>1.5</h1>

The functions you should modify are:

<ul>

 <li>Rope::Rope(…) in rope.cpp</li>

 <li>void Rope::simulateEuler(…) in rope.cpp</li>

 <li>void Rope::simulateVerlet(…) in rope.cpp</li>

 <li><strong>Getting started</strong></li>

</ul>

You need to have OpenGL libraries installed on your system to compile and run. Otherwise, you can use the VM provided. Download the project’s skeleton code, and build the project by using the following commands:

$ mkdir build $ <strong>cd </strong>build $ cmake . .

$ make

After this, you should be able to run the given code by using <strong>./ropesim</strong>.