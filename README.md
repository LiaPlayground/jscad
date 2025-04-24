<!--
author:  André Dietrich

version: 0.0.1

logo:    img/logo.png

script:  https://cdnjs.cloudflare.com/ajax/libs/pako/2.1.0/pako.min.js

comment: This is a LiaScript template for JSCAD, a JavaScript-based 3D modeling library. It allows you to create 3D models using JavaScript code and visualize them in the browser. In this template in particular, uses https://jscad.app to visualize the models.

attribute: [jscad.app](https://jscad.app) was developed by Davor Hrg, follow him on GitHub at <br> https://github.com/hrgdavor  

@JSCAD: @JSCAD_(@uid,```@0```)

@JSCAD_
<script run-once style="display: block" modify="false">
function load() {
    if (!pako) {
        setTimout(load, 100)
        return
    }

    // Compress input string with GZIP
    const compressed = pako.gzip(`@'1`)
    let binary = '';
    for (let i = 0; i < compressed.length; i++) {
      binary += String.fromCharCode(compressed[i]);
    }
    
    send.html(`<div
      style="position: relative; left: 50%; transform: translateX(-50%); resize: both; overflow: auto; height: 64vh; min-height: 320px; display: grid; place-items: center;">
      <iframe allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true" style="margin: 0 auto; width: 100%; height: 100%; border: 1px solid black; overflow: auto;" id="jscad_@0" src="https://jscad.app/#data:application/gzip;base64,${btoa(binary)}"></iframe>
  <button onclick="document.getElementById('jscad_@0').requestFullscreen()" style="position: absolute; bottom: 10px; right: 10px; z-index: 100;">Fullscreen</button>
</div>`)

    send.lia("LIA: stop")
}

load()

"LIA: wait"
</script>

@end

@JSCAD.eval
<script>
function load() {
    if (!pako) {
        setTimeout(load, 100)
        return
    }
    // Compress input string with GZIP
    const compressed = pako.gzip(`@'input`)
    let binary = '';
    for (let i = 0; i < compressed.length; i++) {
      binary += String.fromCharCode(compressed[i]);
    }

    
    console.html(`<div style="resize: both; overflow: hidden; height: 24vh; min-height: 320px"><iframe style="width: 100%; height: 100%; border: 1px solid black" src="https://jscad.app/#data:application/gzip;base64,${btoa(binary)}"></iframe></div>`)

    send.lia("LIA: stop")
}

setTimeout(load, 100)

"LIA: wait"
</script>

@end

-->

# JSCAD - LiaScript Template

                     --{{0}}--
This is a LiaScript template for JSCAD, a JavaScript-based 3D modeling library. It allows you to create 3D models using JavaScript code and visualize them in the browser. In this template in particular, uses https://jscad.app to visualize the models.

Try it on LiaScript:

https://liascript.github.io/course/?https://raw.githubusercontent.com/liaTemplates/jscad/master/README.md

See the project on Github:

https://github.com/liaTemplates/jscad

Tutorial:

https://jscad.app/docs/tutorial-01_gettingStarted.html

                     --{{1}}--
Like with other LiaScript templates, there are three ways to integrate JSCAD, but the easiest way is to copy the defintion from Sec. Implementation.

                       {{1}}
1. Load the latest macros via (this might cause breaking changes)

   import: https://raw.githubusercontent.com/liaTemplates/jscad/main/README.md

   or the current version 0.0.1 via:

   import: https://raw.githubusercontent.com/LiaTemplates/jscad/0.0.1/README.md

2. Copy the definitions into your Project

3. Clone this repository on GitHub

## `@JSCAD`

                     --{{0}}--
The `@JSCAD` macro is used to create a JSCAD model. The code block contains the JavaScript code that defines the 3D model.


```` markdown
``` javascript @JSCAD
// An import statement allows your code to use jscad methods:
const { cube } = require('@jscad/modeling').primitives

// A function declaration that returns geometry
const main = () => {
  return cube()
}

// A declaration of what elements in the module (this file) are externally available.
module.exports = { main }
```
````

Result:


``` javascript @JSCAD
// An import statement allows your code to use jscad methods:
const { cube } = require('@jscad/modeling').primitives

// A function declaration that returns geometry
const main = () => {
  return cube()
}

// A declaration of what elements in the module (this file) are externally available.
module.exports = { main }
```

                     --{{1}}--
For more information about the JSCAD API, see the documentation:

https://openjscad.xyz/dokuwiki/doku.php?id=en:jscad_design_guide

## `@JSCAD.eval`

                        --{{0}}--
Although the `@JSCAD` macro can also be used to inspect and modify the javascript code.The `@JSCAD.eval` macro, is used slightly different. It is attached to the end of the code block. It is used to evaluate the code and display the result in the browser. This way all previous scripts are preserved in a linear versioning system, where the user can go back to previous versions.

```` markdown
``` javascript
// An import statement allows your code to use jscad methods:
const { cube } = require('@jscad/modeling').primitives

// A function declaration that returns geometry
const main = () => {
  return cube()
}

// A declaration of what elements in the module (this file) are externally available.
module.exports = { main }
```
@JSCAD.eval
````

Result:

``` javascript
"use strict"
/**
 * JSCAD Primitives Demonstration
 * Demonstrates the basics of a variety of 2D and 3D primitives
 */

const jscad = require('@jscad/modeling')
const { arc, circle, ellipse, line, polygon, rectangle, roundedRectangle, square, star } = jscad.primitives
const { cube, cuboid, cylinder, cylinderElliptic, ellipsoid, geodesicSphere, roundedCuboid, roundedCylinder, sphere, torus } = jscad.primitives
const { translate } = require('@jscad/modeling').transforms

function main() {
  const shapes = [
    arc({ center: [-1, -1], radius: 2, startAngle: 0, endAngle: (Math.PI / 2), makeTangent: false, segments: 32 }),
    line([[1, 1], [-1, -1], [1, -1]]),
    circle({ radius: 1.8, segments: 10 }),
    ellipse({ radius: [0.7, 2] }),
    polygon({ points: [[-3, -1], [3, -1], [3.5, 2], [1.5, 1], [0, 2], [-1.5, 1], [-3.5, 2]] }),
    rectangle({ size: [2, 3] }),
    roundedRectangle({ size: [4, 3], roundRadius: 0.7 }),
    square({ size: 3.5 }),
    star(),
    star({ vertices: 9, outerRadius: 2, innerRadius: 0.8, density: 2, startAngle: Math.PI / 18 }),

    // cuboids
    cube(),
    cuboid({ size: [1, 2, 3] }),
    roundedCuboid({ size: [2, 3, 2], roundRadius: 0.4, segments: 32 }),
    // spheroids
    sphere({ radius: 2, segments: 12 }),
    sphere({ radius: 2 }),
    geodesicSphere({ radius: 1.5, frequency: 6 }),
    geodesicSphere({ radius: 1.5, frequency: 18 }),
    // ellipsoids
    ellipsoid({ radius: [2, 1, 1.5], segments: 64, axes: [[1, 1, 0], [0, -1, 1], [-1, 0, 1]] }),
    cylinder({ radius: 1, height: 5 }),
    roundedCylinder({ radius: 1, height: 6, roundRadius: 0.8 }),
    cylinderElliptic({ height: 6, startRadius: [1, 1], endRadius: [0, 0] }),
    cylinderElliptic({ height: 6, startRadius: [1, 1.5], endRadius: [1.5, 1] }),
    cylinderElliptic({ height: 6, startRadius: [1, 2], endRadius: [1, 2], startAngle: 0, endAngle: Math.PI / 2 }),
    // torii
    torus({ innerRadius: 1, outerRadius: 1.2 }),
    torus({ innerRadius: 1, outerRadius: 1.5, innerSegments: 4, outerSegments: 6, innerRotation: 0 }),
  ]

  // Arrange primitives in a grid
  return shapes.map((primitive, index) => translate([(index % 5 - 1) * 5, Math.floor(index / 5 - 1) * 5, 0], primitive))
}

module.exports = { main }
```
@JSCAD.eval

                     --{{1}}--
The terminal output can be enlarged by grabbing and dragging the bottom right corner of the terminal window. 

## Implementation

                     --{{0}}--
The implementation of the `@JSCAD` macro is done in the `@JSCAD` macro. The code block contains the JavaScript code that defines the 3D model. The code is then compressed using GZIP and displayed in an iframe.

```` html
script: https://cdnjs.cloudflare.com/ajax/libs/pako/2.1.0/pako.min.js

attribute: [jscad.app](https://jscad.app) was developed by Davor Hrg, follow him on GitHub at <br> https://github.com/hrgdavor  

@JSCAD: @JSCAD_(@uid,```@0```)

@JSCAD_
<script run-once style="display: block" modify="false">
function load() {
    if (!pako) {
        setTimout(load, 100)
        return
    }

    // Compress input string with GZIP
    const compressed = pako.gzip(`@'1`)
    let binary = '';
    for (let i = 0; i < compressed.length; i++) {
      binary += String.fromCharCode(compressed[i]);
    }
    
    send.html(`<div
      style="position: relative; left: 50%; transform: translateX(-50%); resize: both; overflow: auto; height: 64vh; min-height: 320px; display: grid; place-items: center;"><iframe allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true" style="margin: 0 auto; width: 100%; height: 100%; border: 1px solid black; overflow: auto;" id="jscad_@0" src="https://jscad.app/#data:application/gzip;base64,${btoa(binary)}"></iframe><button onclick="document.getElementById('jscad_@0').requestFullscreen()" style="position: absolute; bottom: 10px; right: 10px; z-index: 100;">Fullscreen</button></div>`)

    send.lia("LIA: stop")
}

load()

"LIA: wait"
</script>

@end

@JSCAD.eval
<script>
function load() {
    if (!pako) {
        setTimeout(load, 100)
        return
    }
    // Compress input string with GZIP
    const compressed = pako.gzip(`@'input`)
    let binary = '';
    for (let i = 0; i < compressed.length; i++) {
      binary += String.fromCharCode(compressed[i]);
    }

    console.html(`<div style="resize: both; overflow: hidden; height: 24vh; min-height: 320px"><iframe style="width: 100%; height: 100%; border: 1px solid black" src="https://jscad.app/#data:application/gzip;base64,${btoa(binary)}"></iframe></div>`)

    send.lia("LIA: stop")
}

setTimeout(load, 100)

"LIA: wait"
</script>

@end
````
