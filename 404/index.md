---
title: 404
permalink: /404
permalink: /404/
layout: false 
comments: false
aside: false
top_img: false
footer: true   # ���� Butterfly ҳ��
---
<div id="space-404"></div>

<!-- ��ѡ��������ҳ��ť -->
<a class="back-home" href="/">������ҳ</a>
<!-- �ǿձ�����ʽ -->
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

<!-- 3D �߼� -->
<script type="module">
import * as THREE from 'https://cdn.skypack.dev/three@0.136.0';

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, innerWidth/innerHeight, 0.1, 1000);
const renderer = new THREE.WebGLRenderer({ alpha:true });
renderer.setSize(innerWidth, innerHeight);
document.getElementById('space-404').appendChild(renderer.domElement);

// 20 ��С����
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
    "����·���������˰��顣",
    "404 �ˣ�����ȥдƪ���Ͱɣ�",
    "С����˵�����Ҹ��"
  ][i%3];
  scene.add(mesh);
  asteroids.push(mesh);
}
camera.position.z = 15;

// ���߼����
const raycaster = new THREE.Raycaster();
const mouse = new THREE.Vector2();
addEventListener('click', e=>{
  mouse.x = (e.clientX/innerWidth)*2 - 1;
  mouse.y = -(e.clientY/innerHeight)*2 + 1;
  raycaster.setFromCamera(mouse, camera);
  const inter = raycaster.intersectObjects(asteroids);
  if (inter.length) alert(inter[0].object.userData.joke);
});

// ����ѭ��
function animate(){
  requestAnimationFrame(animate);
  asteroids.forEach(a=>a.rotation.y+=0.01);
  scene.rotation.y += 0.0005;
  renderer.render(scene, camera);
}
animate();

// ���ڴ�С�仯����
addEventListener('resize', ()=>{
  camera.aspect = innerWidth/innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(innerWidth, innerHeight);
});
</script>                                                                                                                                                   