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

# Creating a small scene ( from official docs - rendering a cube )

 To actually be able to display anything with three.js, we need three things: 
 - scene
 - camera
 - renderer

### Project structure

Before setting up the scene , the camera and the renderer make sure you have at least 2 files : a ```index.html``` and a ```main.js```.

- Index. html
```
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8">
		<title>My first three.js app</title>
		<style>
			body { margin: 0; }
		</style>
	</head>
	<body>
		<script type="module" src="/main.js"></script>
	</body>
</html>
````
- main.js

```import * as THREE from 'three';```

### Setting up the elements

- Instatiating the scene :

```js
const scene = new THREE.Scene();
```

- Instatiating the camera :

```js
const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );
```
There are a few different cameras in three.js. For now, let's use a PerspectiveCamera.
- The first attribute is the field of view.
  - FOV is the extent of the scene that is seen on the display at any given moment. 
  - The value is in degrees.

- The second one is the aspect ratio.
  - You almost always want to use the width of the element divided by the height
  - Unless you want the image the image to look squished.

- The next two attributes are the near and far clipping plane.
  - The objects further away from the camera than the value of far or closer than near won't be rendered.  
    
- Instatiating the renderer : 

```js
const renderer = new THREE.WebGLRenderer();
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );
```
-  We set the size at which we want it to render our app.
  -  It's a good idea to use the width and height of the area we want to fill with our app - in this case, the width and height of the browser window.
  -  For performance intensive apps, you can also give setSize smaller values, like window.innerWidth/2 and window.innerHeight/2.
- We add the renderer element to our HTML document.
  - This is a <canvas> element the renderer uses to display the scene to us.

### Creating the cube

```js
const geometry = new THREE.BoxGeometry( 1, 1, 1 );
const material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
const cube = new THREE.Mesh( geometry, material );
scene.add( cube );

camera.position.z = 5;
```

- To create a cube, we need a ```BoxGeometry```.
  - This is an object that contains all the points (vertices) and fill (faces) of the cube.
 - In addition to the geometry, we need a material to color it. Three.js comes with several materials, but we'll stick to the ```MeshBasicMaterial``` for now.
 -  The third thing we need is a ```Mesh```.
    -  A mesh is an object that takes a geometry, and applies a material to it, which we then can insert to our scene, and move freely around.

### Animating the cube

If you insert all the code above into the file you created before we began, you should see a green box. Let's make it all a little more interesting by rotating it.

Add the following code right above the renderer.render call in your animate function:

```js
cube.rotation.x += 0.01;
cube.rotation.y += 0.01;
```

- This will be run every frame (normally 60 times per second), and give the cube a nice rotation animation. 
- Basically, anything you want to move or change while the app is running has to go through the animate loop. 
- You can of course call other functions from there, so that you don't end up with an animate function that's hundreds of lines.

### Final Result

- index.html
```html
<!DOCTYPE html>
<html>
	<head lang="en">
		<meta charset="utf-8">
		<title>My first three.js app</title>
		<style>
			body { margin: 0; }
		</style>
	</head>
	<body>
		<script type="module" src="/main.js"></script>
	</body>
</html>
```
- main.js

```js
import * as THREE from 'three';

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );

const renderer = new THREE.WebGLRenderer();
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );

const geometry = new THREE.BoxGeometry( 1, 1, 1 );
const material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
const cube = new THREE.Mesh( geometry, material );
scene.add( cube );

camera.position.z = 5;

function animate() {
	requestAnimationFrame( animate );

	cube.rotation.x += 0.01;
	cube.rotation.y += 0.01;

	renderer.render( scene, camera );
}

animate();
```
