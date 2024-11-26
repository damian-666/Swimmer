basic poinrt 



with JavaScript that simulates a point mass orbiting around the Earth using Reversible  integration. This will include a canvas to draw the Earth and the orbiting point. We'll also include a camera control to view the scene from different angles.

Here's the HTML file with the JavaScript code:

### Explanation:
1. **Initialization and Constants:**
    - We initialize gravitational constant `G`, Earth’s mass, and Earth’s radius.
    - We set a simulation scale factor to visualize the distances properly.

2. **Simulation Parameters:**
    - Define the time step `dt` for the Verlet integration.
    - Initialize position, velocity, and force vectors.
    - Set initial conditions for altitude and speed.

3. **Canvas Setup:**
    - Create a canvas and set up the WebGL context.
    - Configure the camera angles and distance from the center of the Earth.

4. **Verlet Integration:**
    - Calculate the force due to gravity and apply it to update the position using Verlet integration.

5. **Drawing Function:**
    - Draw the Earth and the orbiting point mass on the canvas.
    - Project 3D positions to 2D for visualization.

6. **Animation Loop:**
    - Continuously update the position of the point mass and redraw the scene.

7. **Camera Control:**
    - Add mouse event listeners to control the camera angle.

This example sets up a basic simulation of a point mass orbiting the Earth. You can expand upon this by adding more complex dynamics, rigid body physics, and other features as needed.

Feel free to build upon this foundation to achieve your specific goals!
