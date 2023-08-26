# ThreeJS_Fundamentals

This README is used as a personal guide to take notes on what I found important. 

More detailed explanations are on the official docs : https://threejs.org/docs/index.html#manual/en/introduction/Installation

# The basic structure of threeJS app

![image](https://github.com/izzypt/ThreeJS_Fundamentals/assets/73948790/7247a0bc-7370-4be4-9d95-7dc00a314895)

### The elments:

- There is a <in>Renderer</ins>.
  - This is arguably the main object of three.js.
  - You pass a Scene and a Camera to a Renderer and it renders (draws) the portion of the 3D scene that is inside the frustum of the camera as a 2D image to a canvas.
