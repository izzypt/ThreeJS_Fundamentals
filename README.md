# ThreeJS_Fundamentals

This README is used as a personal guide to take notes on what I found important. 

More detailed explanations are on the official docs : https://threejs.org/docs/index.html#manual/en/introduction/Installation

# The basic structure of threeJS app

![image](https://github.com/izzypt/ThreeJS_Fundamentals/assets/73948790/9dc68d16-30fd-4650-94dc-6ca78e9130fa)


### The elements:

- ***Renderer***
  - This is arguably the main object of three.js.
  - You pass a Scene and a Camera to a Renderer and it renders (draws) the portion of the 3D scene that is inside the frustum of the camera as a 2D image to a canvas.
- ***SceneGraph***
  -  It's a tree like structure, consisting of various objects like a Scene object, multiple Mesh objects, Light objects, Group, Object3D, and Camera objects.
  -  A ***Scene*** object defines the root of the scenegraph and contains properties like the background color and fog.
  -  These objects define a hierarchical parent/child tree like structure and represent where objects appear and how they are oriented.
  -  Children are positioned and oriented relative to their parent.
  -  For example the wheels on a car might be children of the car so that moving and orienting the car's object automatically moves the wheels.
- ***Camera***
  -  In three.js, unlike the other objects, a Camera does not have to be in the scenegraph to function.
  -  Just like other objects, a Camera, as a child of some other object, will move and orient relative to its parent object.
- ***Mesh***
  -   Represent drawing a specific ***Geometry*** with a specific ***Material***.
  - Both ***Material*** objects and ***Geometry*** objects can be used by multiple Mesh objects.
  - For example to draw two blue cubes in different locations we could need two Mesh objects to represent the position and orientation of each cube.
- ***Geometry***
  -  Represent the vertex data of some piece of geometry like a sphere, cube, plane, dog, cat, human, tree, building, etc...
  -  Three.js provides many kinds of built in geometry primitives. You can also create custom geometry as well as load geometry from files.
- ***Material***
  -  Represent the surface properties used to draw geometry including things like the color to use and how shiny it is.
  -  A Material can also reference one or more Texture objects which can be used, for example, to wrap an image onto the surface of a geometry.
- ***Texture***     
  -  Objects generally represent images either loaded from image files, generated from a canvas or rendered from another scene.
