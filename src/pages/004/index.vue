<route lang="yaml">
name: 等速の変化
meta: 
  order: 4
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
  let d = $ref(0)
  let bgColor: P5.Color = $ref(p.color(p.random(255), p.random(255), p.random(255)))
  let circleColor: P5.Color = $ref(p.color(p.random(255), p.random(255), p.random(255)))

  function reset() {
    bgColor = circleColor
    circleColor = p.color(p.random(255), p.random(255), p.random(255))
    d = 0
  }
  p.setup = () => {
    p.createCanvas(p.windowWidth, p.windowHeight)
    p.noStroke()
  }
  p.draw = () => {
    d += 2
    if (d / 2 > p.dist(0, 0, p.width / 2, p.height / 2)) {
      reset()
    }
    p.clear(0, 0, 0, 0)
    p.background(bgColor)
    p.fill(circleColor)
    p.circle(p.width / 2, p.height / 2, d)
  }
  p.windowResized = () => {
    p.resizeCanvas(p.windowWidth, p.windowHeight)
  }
  p.mouseClicked = () => {
    reset()
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
