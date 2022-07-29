<route lang="yaml">
name: クランプ
meta: 
  order: 7
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
  }
  p.draw = () => {
    p.clear(0, 0, 0, 0)
    p.stroke('red')
    p.line(100, 0, 100, p.height)
    p.line(p.width - 100, 0, p.width - 100, p.height)
    p.stroke(240)
    p.line(p.constrain(p.mouseX, 100, p.width - 100), 0, p.constrain(p.mouseX, 100, p.width - 100), p.height)
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
