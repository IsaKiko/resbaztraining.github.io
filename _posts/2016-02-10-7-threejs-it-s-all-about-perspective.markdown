---
published: true
title: 7 - ThreeJS - It's all about perspective
layout: post
---

_Learning objectives:_

* understand the perspective of the camera.
* set the position of mesh and camera.
* adding axes.

At the moment, we're only seeing half the brain. To fix that, we'll need to understand our camera a little bit better. 
When we initiated the camera, we gave it some default parameters. If we look at the [ThreeJS documentation](http://threejs.org/docs/api/cameras/PerspectiveCamera.html) we find out what parameters we have to pass to the camera:
{%highlight javascript%}
PerspectiveCamera( fov, aspect, near, far )
{%endhighlight%}
`fov` is the view angle, `aspect` the aspect ratio, and `near` and `far` set the range of things you can see in the scene. This image might help to get a better understanding about what's going on [1]:
![https://www3.ntu.edu.sg/home/ehchua/programming/opengl/CG_BasicsTheory.html](https://www3.ntu.edu.sg/home/ehchua/programming/opengl/images/Graphics3D_CameraPerspective.png "camera setup")

___

_Challenge: Play with the camera_

Play with the camera settings until you can see the entire brain on the screen. 
...try setting `near = 80`. What happens?

___ 

One thing that you might have noticed while playing with the camera is that you always look at the brain from the same direction. All we know how to change are the distance and the aspect ratio. Let's have a look at where our camera actually is by printing its position in the console:
{%highlight javascript%}
console.log(camera.position);
{%endhighlight%}

Now we can set the camera position using `camera.position.set()` and giving it an x, y, and z coordinate:

{%highlight javascript%}
camera.position.set( 20, 20, 120 );
{%endhighlight%}

One important thing I want to have if I'm in a 3D space is a reference system. ThreeJS doesn't come with a simple command to create axes, so we wrote a little script to help us with this. It should be in your `/js` folder. To use it, we'll have to load it in the `index.html`. It needs to be included before the `main.js`, so we have access to its functionality in our main file.   

{%highlight html%}
<script src="js/three.min.js"></script>
<script src="js/STLLoader.js"></script>
<script src="js/makeAxes.js"></script> <!--  this one -->
<script src="js/main.js"></script>
{%endhighlight%}

To add the axes to the scene, call `addAxes(scene)` any time after creating the scene. 
{%highlight javascript%}
addAxes(scene);
{%endhighlight%}

___

_Challenge:_
Move the camera over the brain, onto the z-axis. What are we looking at now?

___

If we move the camera, it miraculously focusses on the brain again. If we don't want that, but want the default view when we load the page to be something else, we can tell it to look at any other point in the coordinate system instead, using `camera.lookAt()`. This command is used with a ThreeJS vector, which is just another way of sayin "this point in space". We'll come across more of these vectors later. We can either initialise it as a variable like we're used to, or we can create a new one on the fly (which is what we'll do here, because we won't need it a second time):

{%highlight javascript%}
camera.lookAt( new THREE.Vector3( 100, 10, 10 ) );
{%endhighlight%}

___

_Challenge:_
Similar to setting the positon, we can rotate the camera around the x-, y-, and z-axis. 
Inspecting what `console.log(camera.rotation);`
returns, think of how you could just modify the rotation around the x-axis?

___

Sooo... we could play with this for ever, create buttons to rotate, focus, zoom, and pan. But instead, we'll rely on a pre-built library that has all these controls conveniently packaged up already.

[1] [https://www3.ntu.edu.sg/home/ehchua/programming/opengl/CG_BasicsTheory.html](Frustrum image reference)