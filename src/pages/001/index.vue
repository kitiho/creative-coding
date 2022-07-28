<route lang="yaml">
name: 準備
meta: 
  order: 1
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
    p.circle(p.width / 2, p.height / 2, 50)
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
