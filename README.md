
This is a simulation of a black hole and particles representing stars moving around it. It uses Pygame to display the simulation on a window of size WINDOW_SIZE = (1800, 1000).

The simulation uses the formula for gravitational force to calculate the acceleration of each particle due to other particles and the black hole. The velocity and position of each particle are then updated based on the acceleration.

The simulation also stores the positions of each particle over time and draws a line to show the particle's trajectory. The black hole is represented as a circle with a chosen radius in the center of the screen. The particles representing stars are also drawn as circles with a random radius.

The simulation runs in a loop until the user closes the Pygame window.

it uses following modules:import, random, math

