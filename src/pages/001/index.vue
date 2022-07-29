<route lang="yaml">
name: 準備
meta: 
  order: 1
</route>
<script setup lang="ts">
import P5 from 'p5'
import { onMounted, ref } from 'vue';
function init() {
  new P5(sketch)
}

function sketch(p: P5) {
  p.setup = () => {
    const canvas = p.createCanvas(400, 400)
    canvas.style('margin', '16px')
    canvas.parent('#container')
    p.background(103, 107, 121)
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
  <div id="container" />
</template>

<style scoped >
#container {
  width: 100%;
  height: 100%;
  background: #292a33;
  overflow: hidden;
}
</style>
