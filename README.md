# three-screen-quad
a screen aligned quad for three.js



[![stable](http://badges.github.io/stability-badges/dist/stable.svg)](http://github.com/badges/stability-badges)

ThreeJS element for drawing stuff to screen. See [test](#testing) for an example.

```js
var THREE = require('three')
var ScreenQuad = require('three-screen-quad')(THREE)

var screenQuad;

function start(gl, width, height) {

    renderer = new THREE.WebGLRenderer({
        canvas: gl.canvas
    });

    scene = new THREE.Scene();
    
    camera = new THREE.PerspectiveCamera(50, width/height, 1, 1000);
    
    camera.position.set( 0 , 0 , -10 );

    camera.lookAt( new THREE.Vector3() )

    //will make a quad thats 25% of the screen size in both directions
    //offset in pixels from top left corner 

    screenQuad = new ScreenQuad({
    	width: 0.25,
    	height: 0.25,
    	top: '25px',
    	left: '25px'
    });

    screenQuad.setScreenSize( renderer.getSize().width , renderer.getSize().height );

    scene.add(screenQuad);

}

function render(gl, width, height) {
    renderer.render(scene, camera)
}

function onWindowResize( width , height ){
	
	//if a value is set in pixels, the canvas size needs to be set on the element
	screenQuad.setScreenSize( width , height );

}
```

## Usage
[![NPM](https://nodei.co/npm/three-screen-quad.png)](https://npmjs.org/package/three-screen-quad)

#### `ScreenQuad = require('three-screen-quad')(THREE)`

This module exports a function which accepts an instance of THREE, and returns a ScreenQuad class. This allows you to use the module with CommonJS, globals, etc.

The returned function has the following constructor pattern:

```js
screenQuad = new OrbitControls({
	width: 	0.5, 
	height: '50px',
	top:    0.25, 
	left:   '25px'
})
```

##methods

**setWidth( float | string )** - width of the element. 

**setHeight( float | string )** - height of the element. 

**setTop( float | string )** - distance from top of the canvas. 

**setLeft( float | string )** - distance from the left edge of the canvas. 

**setOffset( top , left )** - sets both top and left at the same time

**setSize( width , height )** - sets both width and height at the same time

_(Each argument can be either a float (representing percentage 0.0 - 1.0), or string (for pixel size '25px' ))_;

**setScreenSize( width , height )** - sets the screensize in pixels, should be called when the canvas resizes, needed if there are any pixel values assigned

## testing

Git clone, `npm install` and then run `npm start` to spin up a development server. Open `localhost:9966` in your browser to see the `test.js` file in action.
