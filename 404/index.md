---
title: 404
permalink: /404
permalink: /404/
layout: false 
comments: false
aside: false
top_img: false
footer: true   # 保留 Butterfly 页脚
---
<div id="space-404"></div>

<!-- 可选：返回首页按钮 -->
<a class="back-home" href="/">返回首页</a>
<!-- 星空背景样式 -->
<style>
#space-404{
  position:fixed;top:0;left:0;width:100vw;height:100vh;
  background:radial-gradient(circle,#0f0c29,#302b63,#24243e);
  z-index:-1;
}
.back-home{
  position:absolute;top:20px;left:20px;
  color:#fff;background:rgba(255,255,255,.1);
  padding:8px 16px;border-radius:4px;text-decoration:none;
  z-index:10;
}
</style>

<!-- 3D 逻辑 -->
<script type="module">
import * as THREE from 'https://cdn.skypack.dev/three@0.136.0';

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, innerWidth/innerHeight, 0.1, 1000);
const renderer = new THREE.WebGLRenderer({ alpha:true });
renderer.setSize(innerWidth, innerHeight);
document.getElementById('space-404').appendChild(renderer.domElement);

// 20 颗小行星
const asteroids = [];
for (let i=0; i<20; i++){
  const mesh = new THREE.Mesh(
    new THREE.SphereGeometry(Math.random()*0.4+0.1, 16, 16),
    new THREE.MeshBasicMaterial({ color:0xffffff, wireframe:true })
  );
  mesh.position.set(
    (Math.random()-0.5)*30,
    (Math.random()-0.5)*20,
    (Math.random()-0.5)*30
  );
  mesh.userData.joke = [
    "你迷路的样子像极了爱情。",
    "404 了？不如去写篇博客吧！",
    "小行星说：点我干嘛？"
  ][i%3];
  scene.add(mesh);
  asteroids.push(mesh);
}
camera.position.z = 15;

// 射线检测点击
const raycaster = new THREE.Raycaster();
const mouse = new THREE.Vector2();
addEventListener('click', e=>{
  mouse.x = (e.clientX/innerWidth)*2 - 1;
  mouse.y = -(e.clientY/innerHeight)*2 + 1;
  raycaster.setFromCamera(mouse, camera);
  const inter = raycaster.intersectObjects(asteroids);
  if (inter.length) alert(inter[0].object.userData.joke);
});

// 动画循环
function animate(){
  requestAnimationFrame(animate);
  asteroids.forEach(a=>a.rotation.y+=0.01);
  scene.rotation.y += 0.0005;
  renderer.render(scene, camera);
}
animate();

// 窗口大小变化适配
addEventListener('resize', ()=>{
  camera.aspect = innerWidth/innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(innerWidth, innerHeight);
});
</script>                                                                                                                                                   