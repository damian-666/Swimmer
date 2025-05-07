# Advanced Physics Simulation Coding Prompt

## Objective
Create a precise, maintainable, and well-documented orbital physics simulation using modern web technologies.

## Core Requirements
1. **Programming Language**: JavaScript (or TypeScript if advantageous)
2. **Rendering Framework**: Three.js
3. **Architecture**: Producer-consumer loop with separate calculation and rendering threads
4. **Performance**: Use SIMD if available in JS

## Documentation Standard
```javascript
// ====================
// Units Dictionary
// ====================
/**
 * @type {Object<string, string>}
 * Central reference for all units used in the simulation
 */
const UNITS = {
    // Physical constants
    length: 'meters',
    mass: 'kg',
    time: 'seconds',
    force: 'N',
    // Derived units
    velocity: 'm/s',
    acceleration: 'm/s²'
};
```

All functions must use JSDoc with comprehensive metadata:

```javascript
/**
 * Calculates gravitational force between two bodies
 *
 * @param {number} mass1 - Mass of first body [kg]
 * @param {number} mass2 - Mass of second body [kg]
 * @param {number} distance - Distance between centers of mass [m]
 * @returns {number} Force magnitude [N]
 * @throws {RangeError} If distance is zero or negative
 *
 * @example
 *     const force = calculateGravitationalForce(5.97e24, 7.35e22, 384.4e6);
 */
```

## Design Principles

1. **Separation of Concerns**:
   - Model (physics) must never reference View (rendering)
   - View may reference Model to display state
   - Transformations follow: Model Space → Transform → View Space

2. **Numerical Precision**:
   - Use floating point for standard calculations
   - Use fixed-point for reversible integrators:
     ```javascript
     // Fixed-point implementation (24.8 format)
     const FIXED_POINT_FACTOR = 256; // 2^8
     const fixedPos = Math.round(floatPos * FIXED_POINT_FACTOR);
     ```

3. **Error Handling**:
   - Catch all exceptions with line numbers and descriptions
   - If an exception occurs, fix it and retry up to 3 times before asking for help

## Camera & Visualization

1. **Camera System**:
   - Implement orthographic camera for top-down view
   - Create bounding box view that ensures all objects remain visible
   - Add hotkeys (1,2,3) for different views (top, side, front, back)
   - Enable object tracking without changing zoom factor

2. **Coordinate Transformation**:
   - Implement 2×2 invertible matrix for view-to-model transformations
   - Display mouse position in world units (km, m)

## Physics Implementation

1. **Integration Method**:
   - When marked "reversible" in title, use Jos Stam's integer/fixed-point reversible solver
   - Otherwise, use Position Verlet algorithm for energy conservation
   - Ensure all forces have equal and opposite reactions

2. **Constraints**:
   - Implement distance constraints for tethers, following this pattern:
   ```javascript
   /**
    * Connects two bodies at given offset points
    * @class PointToPointConstraint
    * @param {Body} bodyA - First body
    * @param {Vec3} pivotA - Point relative to center of mass of bodyA
    * @param {Body} bodyB - Second body
    * @param {Vec3} pivotB - Point relative to center of mass of bodyB
    * @param {Number} maxForce - Maximum constraint force [N]
    */
   ```

## Simulation Specifics

The simulation models a 3-body system:
1. **Earth**: Central gravitational body
2. **Satellite**: Cone-shaped body (100kg) in initial circular LEO at 500km
3. **Kicker**: Cylindrical mass (20kg) attached to satellite via tether

The simulation should demonstrate the Oberth effect by:
1. Starting with circular orbit
2. Applying impulse at perigee
3. Allowing kicker to reach maximum distance
4. Retracting tether gradually (ideally over half the orbital period)
5. Observing energy and eccentricity changes

## Development Workflow

1. Begin with boilerplate code including Three.js and OrbitControls
2. Implement core physics without complex engines
3. Test frequently and fix errors immediately
4. Avoid repetition and magic numbers
5. Use proper object structures for related parameters (position, velocity, mass)

## Success Criteria

1. Functioning orbital mechanics with proper gravitational calculations
2. Visible demonstration of orbital changes after impulse
3. Clear visualization with proper camera controls and coordinate display
4. Well-documented, maintainable code structure
5. No blank screens or unhandled errors
