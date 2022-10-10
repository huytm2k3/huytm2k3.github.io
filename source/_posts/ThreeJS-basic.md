---
title: ThreeJS basic
date: 2022-10-10 07:30:36
tags: [front-end]
---

## ThreeJS là gì?

ThreeJs là framework lập trình 3D cho Web trên webGL, (openGL).
Để bắt đầu với ThreeJs, bạn cần có kiến thức vững về web, #html5, và #javascript
Cơ bản ThreeJS bao gồm tất cả API 3d của WebGL, giúp người lậ p trình có thể dễ dàng lập trình 3D trên môi trường web. ThreeJs render với html5 #canvas

## Getting Started

### CDN

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/0.145.0/three.min.js"></script>
```

### Selector

```js
const canvas = document.querySelector("#c");
const renderer = new THREE.WebGLRenderer({ canvas });
```

### Define Camera

```js
const fov = 75;
const aspect = 2; // the canvas default
const near = 0.1;
const far = 5;
const camera = new THREE.PerspectiveCamera(fov, aspect, near, far);
camera.position.z = 2;
```

### Define scene

```js
const fov = 75;
const aspect = 2; // the canvas default
const near = 0.1;
const far = 5;
const camera = new THREE.PerspectiveCamera(fov, aspect, near, far);
camera.position.z = 2;
```

### Define Object

```js
const boxWidth = 1;
const boxHeight = 1;
const boxDepth = 1;
const geometry = new THREE.BoxGeometry(boxWidth, boxHeight, boxDepth);

const material = new THREE.MeshPhongMaterial({ color: 0x44aa88 }); // greenish blue

const cube = new THREE.Mesh(geometry, material);
scene.add(cube);
```

### Animation

```js
function render(time) {
  time *= 0.001; // convert time to seconds

  cube.rotation.x = time;
  cube.rotation.y = time;

  renderer.render(scene, camera);

  requestAnimationFrame(render);
}
requestAnimationFrame(render);
```
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/0.145.0/three.min.js"></script>
<center><canvas id="c"></canvas></center>

<script>
    'use strict';

    /* global THREE */

    function main() {
        const canvas = document.querySelector('#c');
        const renderer = new THREE.WebGLRenderer({ canvas });

        // Set camera

        const fov = 75;
        const aspect = 2;  // the canvas default
        const near = 0.1;
        const far = 5;
        const camera = new THREE.PerspectiveCamera(fov, aspect, near, far);
        camera.position.z = 2;

        const scene = new THREE.Scene();

        {
            const color = 0xFFFFFF;
            const intensity = 1;
            const light = new THREE.DirectionalLight(color, intensity);
            light.position.set(-1, 2, 4);
            scene.add(light);
        }

        // Define object

        const boxWidth = 1;
        const boxHeight = 1;
        const boxDepth = 1;
        const geometry = new THREE.BoxGeometry(boxWidth, boxHeight, boxDepth);

        const material = new THREE.MeshPhongMaterial({ color: 0x44aa88 });  // greenish blue

        const cube = new THREE.Mesh(geometry, material);
        scene.add(cube);

        function render(time) {
            time *= 0.001;  // convert time to seconds

            cube.rotation.x = time;
            cube.rotation.y = time;

            renderer.render(scene, camera);

            requestAnimationFrame(render);
        }
        requestAnimationFrame(render);

    }

    main();

</script>

## Three Responsive

https://r105.threejsfundamentals.org/threejs/lessons/threejs-responsive.html

## Three Primitives

https://r105.threejsfundamentals.org/threejs/lessons/threejs-primitives.html