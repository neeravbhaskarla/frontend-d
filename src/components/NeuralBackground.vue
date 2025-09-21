<template>
  <canvas ref="canvas" class="neural-canvas"></canvas>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

const canvas = ref(null);
let ctx, width, height, nodes;

function resize() {
  width = (canvas.value.width = window.innerWidth);
  height = (canvas.value.height = window.innerHeight);
}

function initNodes() {
  const rand = Math.random;
  nodes = Array.from({ length: 50 }, () => ({
    x: rand() * width,
    y: rand() * height,
    vx: (rand() - 0.5) * 0.6,
    vy: (rand() - 0.5) * 0.6,
    r: 2 + rand() * 1.5,
  }));
}

function animate() {
  ctx.clearRect(0, 0, width, height);

  // Draw connections
  for (let i = 0; i < nodes.length; i++) {
    for (let j = i + 1; j < nodes.length; j++) {
      let dx = nodes[i].x - nodes[j].x;
      let dy = nodes[i].y - nodes[j].y;
      let dist = Math.sqrt(dx * dx + dy * dy);
      if (dist < 200) {
        ctx.strokeStyle = `rgba(255,255,255,0.4)`;
        ctx.lineWidth = 0.5;
        ctx.beginPath();
        ctx.moveTo(nodes[i].x, nodes[i].y);
        ctx.lineTo(nodes[j].x, nodes[j].y);
        ctx.stroke();
      }
    }
  }

  // Draw nodes
  for (let node of nodes) {
    ctx.beginPath();
    ctx.arc(node.x, node.y, node.r, 0, Math.PI * 2);
    ctx.fillStyle = "rgba(255,255,255,0.5)";
    ctx.fill();

    node.x += node.vx;
    node.y += node.vy;
    if (node.x < 0 || node.x > width) node.vx *= -1;
    if (node.y < 0 || node.y > height) node.vy *= -1;
  }

  requestAnimationFrame(animate);
}

onMounted(() => {
  ctx = canvas.value.getContext("2d");
  resize();
  initNodes();
  window.addEventListener("resize", resize);
  animate();
});

onBeforeUnmount(() => {
  window.removeEventListener("resize", resize);
});
</script>

<style scoped>
.neural-canvas {
  position: fixed;
  inset: 0;
  width: 100%;
  height: 100%;
  display: block;
  background: #000;
}
</style>
