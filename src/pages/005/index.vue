<route lang="yaml">
name: 色の指定
meta: 
  order: 5
</route>
<script setup lang="ts">
import P5 from 'p5'
import { onMounted, ref } from 'vue';
import { $ref } from 'vue/macros';
const container = ref()
function init() {
  new P5(sketch, container.value)
}

function sketch(p: P5) {
  p.setup = () => {
    p.createCanvas(p.windowWidth, p.windowHeight)
    p.fill(255);
    p.circle(p.width / 2 - 50, p.height / 4, 50);

    p.fill(255, 128);
    p.circle(p.width / 2 + 50, p.height / 4, 50);

    p.fill(255, 0, 0);
    p.circle(p.width / 2 - 50, (p.height / 4) * 2, 50);

    p.fill(255, 0, 0, 128);
    p.circle(p.width / 2 + 50, (p.height / 4) * 2, 50);

    p.colorMode(p.HSB);
    p.fill(100, 100, 100);
    p.circle(p.width / 2 - 50, (p.height / 4) * 3, 50);

    p.fill(100, 100, 100, 0.5);
    p.circle(p.width / 2 + 50, (p.height / 4) * 3, 50);

    p.colorMode(p.HSB, p.width, 100, 100)
  }
  p.draw = () => {
    p.fill(p.mouseX, 100, 100)
    p.circle(p.mouseX, p.mouseY, 40)
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
