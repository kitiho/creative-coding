<route lang="yaml">
name: 円の描画
meta: 
  order: 3
</route>
<script setup lang="ts">
import P5 from 'p5'
import { onMounted, ref } from 'vue';
const container = ref()
function init() {
  new P5(sketch, container.value)
}
function sketch(p: P5) {
  p.setup = () => {
    p.createCanvas(p.windowWidth, p.windowHeight)
    p.strokeWeight(10)
    p.stroke(240)
    p.noFill()
    p.circle(p.width / 5, p.height / 2, 100)

    p.noStroke();
    p.fill(240);
    p.circle(p.width / 5 * 2, p.height / 2, 100);

  }

  p.draw = () => {
    // p.stroke(0)
    // p.strokeWeight(1)
    // p.circle(p.mouseX, p.mouseY, p.random(100));

    if (p.frameCount % 10 === 0) {
      p.noFill()

      p.strokeWeight(p.random(1, 5));
      p.stroke(p.random(180, 255));
      p.circle(p.width / 5 * 3, p.height / 2, p.random(50, 100));

      p.strokeWeight(1)
      p.ellipse(p.width / 5 * 4, p.height / 2, p.random(100, 200), p.random(100, 200));
    }
  }
  p.windowResized = () => {
    p.resizeCanvas(p.windowWidth, p.windowHeight)
  }
}
onMounted(() => {
  init()
})
</script>
<template>
  <div ref="container" id="canvas" />
</template>

<style scoped>
#canvas {
  background: #292a33;
  overflow: hidden;
}
</style>
