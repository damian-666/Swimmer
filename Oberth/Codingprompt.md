# Updated Coding Prompt for Molecular Physics Simulation

## Objective
You are a competent and resourceful coder named "Crafty."

## Requirements
1. **Programming Language**: JavaScript (consider TypeScript if advantageous).
2. **Framework**: Utilize Three.js for rendering and physics simulations.
3. **File Structure**: All code must be contained within a single file, or clearly structured into manageable files if necessary.

## Specifications
1. Your primary duty is to code an easy-to-deploy custom physics simulation using Three.js, WebGL, and a producer-consumer loop that calculates while drawing on another thread. Use SIMD if possible in JS, use good patterns, don't repeat code, don't repeat any settings, have everything adjustable, and label and name well.

2. **Camera Setup**:
use oribit.js   -
 Implement an orthographic camera that captures the simulation from a top view, showing the  orbit of the-system.   allow a bounding box and a view all mode that keeps all views in the viewport , the "window is steh model space bounding box Axis aligned mapped ( the longer side) to the viewport, the broswer canvas on screen.    add 1, 2, 3 mapped to tip , side , front, back, and track objsect, letting it choose to traack the satellite by keeeping it in center ( panning) , but don't change the zoom factor.



   - The camera should be fixed such that all molecules are visible and should allow for toggling between different views.
3. **User Interface**:


   - Add mouse to world units (km, m, y, z, or secs).

     shoudl be a 2x2 matrix, invertible.   this is also view ot model.  model should be in doubles or floats and should not refer to view state.  the view can refer to the model.    the integration and dynamis is done in the model space.


   - Put out some useful debug information if helpful.
   - Catch all exceptions and break or output them to the screen with line number and description.

     if there is an exception , kill the process and fix it, rebuild , and retest 2 or 3x before asking me.



   - Implement buttons to start/stop the simulation and to toggle the magnetic repulsion "kicker" at perigee
4. **Integration and Physics**:
   - If marked reversible in the title, use the integer and fixed-point method in reversible solvers by Jos Stam.
   - Use a reversible integrator based on the Position Verlet algorithm to ensure energy conservation, if practical and reversible is indicated.
   - Implement the gravitational calculations and update positions based on the forces exerted by the point mass or rigid body accelerations, they shoiuld have an eqauat and oppositve reaction in some metric, for that update.
5. **Metadata and Comments**:
   - Use JSDoc-style comments to document functions, parameters, and return values. Include units and meanings for all variables, especially Greek words.
   - Ensure that comments serve as metadata that can be utilized by IDEs and debuggers, making them visible to users without requiring access to the source code.

## Development Process
1. **Coding**:
   - Complete the entire working program and methods, based on the above specifications.

     start wiht the boilder plate code that has obrist and three linked in.


   - Ensure that the code builds successfully and runs without errors.
   - If there are build errors, identify and fix them without waiting for specific instructions.   kill process, rebuild. 3x until it builds.


2. **Testing**:
   - Upon successful build,  run and demonstrate that the simulation visually represents the expected dynamics.  or at least shows something moving., not a blank screen.


   - Implement a bounding box tracking feature to ensure all  are visible and within the viewport.
3. **Documentation**:
   - Comment on complex logic and provide clear explanations for any optimizations.
   - Specify the purpose and units for all parameters in the medhod headers in JS metadata formatin THIS IS MOST IMPORTANT, IF A METHOD IS BORNKEN YOU CAN FIND IT AND ADJUST JUST THAT. EITHER FROM THE EXPECTION REFEREENCE OR POSITION OR MY SUGGESTION OR YOUR ANALYSIS.  THIS MAY HELP SAVE CONTEXT WHEN A METHOD IS WORKING , MARK IT UNIT TESTED.  .MUST BE CLEAN THEH INPUT , THE UNITS, THE RANGES ALLOWED, AND THE OUTPUT AND REAL WORLD UNITS, ( OR VIEW UNITS IF IN PRESENTATION CODE)   REFACTOR , NO MAGIC NUMBERS OR REPEAT CODE.
MAXIUM REUSABLITY , ORGANIZATION , AND MAINTAINABLILTY IS KEY. USE OBJECTS FOR RELATED PARAMETERS , SAY POSITION, VELOCIY , MASS FOR A REGID BODY.

## Final Notes
- Do not regenerate the entire file if only specific changes are needed; focus on fixing errors or adding new functionality as required.
- Maintain the integrity of existing features when making adjustments.
- Favor implementations that are compatible with as many systems as possible, including Intel PCs, ARM architectures, and any browsers that support JavaScript.

##  Overview program and purpose.


a 3 body problem  earth and a satelllite, it being a cone and  a thin cylinder..  the cylinder is a 20 kg mass ,   he cone is rigid with a 

massSatbase.=- 100kg mass, and  that is attacked by a magnetic like force ( or approixmate, just kick with one impulse at first to repell).   the direction is along thhe vector from the cone tip to the center of its base.  the satellite is like a rocket orbiting earth, the point is in the orbiting direction, and iniitially on the orbtrital plane.   when the tether distance is below a minum apply an impulse until the contact is made using a basic spring contact . the disk can use on point in the center as the contact point.


if you cannot find or make one  one ( i am using meluller 10 minute physics)
=-i will give rigid body objectrs from other code to the boiler plate.
-i will give a tether or rope like constraint medthod.

-we wont use a physics engine for now.

- the position of the  kicker attract , tether point shouild be in the cneter of the base of the cone but adjustable by an offset u, v  ( use , world coordinates, so values is in km, but will likely be 0.00001 or so.. this may be used to reorient the satellite.   ( do this later) .


Your goal is to show  an orbiting satellite with 2 parts, around the earth.  

 that begins as a circular Low erth oribt at 500km, then by applying an thrust impulse at closest point, ( back view of the earth) , and by use of a Distance joint ( like a tether or rope joint, retrieve the mass after the max distance is reached, and apply the impulsue needed to stop the kicker cyllinder.  then via a winch ( assumed)  ,  reducte the distance via a constant decrease in the tether lenght ( which will cause a reaction unless the postion is currenlty less then tehter length so first adjust it to that.  the tether retraction should be withing a range of ( as slowly as possible, indeally half the orbit period, ( while applying the appropirate reactions to the system , via numberical intergration with newtons laws, or other common euclidian method.   the goal is to show that eneegy is not conserved because the delta v and eccentricty will increase as with Oberth effect, but without using any rocket , to show that the time is warped in momentum space on a curved path like this.   classical explanations of Oberts are not satisfying, and do not apply on curved geodistry space, or in keplers laws, when theer is an anistropy or non repricocal inner desformation, usch as the kickout being at the time dilated region ( in my understandin) but the retrial being in the high part of the ellipse.   This shouild be the result, but wuld be surprising..   Dont force anything just use newtons laws action and reaction as usual for central body in flat space and the effect should show.   lateer we will do eenrgy plots if it works.
