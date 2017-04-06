# there.js demo

记录学习过程中的问题

### render多次

有这样一段简单的例子
```javascript
var scene = new THREE.Scene();

var camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);

var renderer = new THREE.WebGLRenderer();

renderer.setSize(window.innerWidth, window.innerHeight);

document.body.appendChild(renderer.domElement);
var geometry = new THREE.CubeGeometry(1,1,1);
var material = new THREE.MeshBasicMaterial({color: 0x00ff00});
var cube = new THREE.Mesh(geometry, material); scene.add(cube);
camera.position.z = 5;
function render() {
    requestAnimationFrame(render);
    cube.rotation.x += 0.1;
    cube.rotation.y += 0.1;
    renderer.render(scene, camera);
}
render();
```

其中有这么一句`renderer.setSize(window.innerWidth, window.innerHeight)`，这是指定当前这个3d对象渲染出来的大小，如果屏幕尺寸改变了，尺寸并不会跟着变。
于是，我在 `window.onresize` 事件中这样做：

```
window.onresize = function () {
    renderer.render(scene, camera);
}
```

结果，动画变得很快，没有达到预期的目的。上面的代码跟下面的差不多
```
// 省略若干
function render() {
    requestAnimationFrame(render);
    cube.rotation.x += 0.1;
    cube.rotation.y += 0.1;
    renderer.render(scene, camera);
}
render();
render();
render();
render();
```

### Performance  的作用

### stats 的使用