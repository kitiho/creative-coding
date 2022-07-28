<route lang="yaml">
name: アニメーション
meta: 
  order: 2
</route>
<script setup lang="ts">
import aaa from './index.vue'
import P5 from 'p5'
import { onMounted, ref } from 'vue';
import { $ref } from 'vue/macros'
console.log(aaa)
const container = ref()
let r = $ref(0)
let x = $ref(0)
let s = $ref("0")
function init() {
  new P5(sketch, container.value)
}
function sketch(p: P5) {
  p.frameCount
  p.setup = () => {
    p.createCanvas(p.windowWidth, p.windowHeight)
    r = p.min(p.width, p.height) / 6
    
    x = r
    s = "0"
  }
  p.draw = () => {
    x += 10;
    if (x > p.width + r) {
      x = -r;
    }
    p.clear(0, 0, 0, 0)
    p.circle(x, p.height / 2, r * 2)
    if (p.frameCount % 30 === 0) {
      s = p.frameRate().toFixed()
    }
    p.push()
    p.noStroke()
    p.fill(240)
    p.text(s, 20, 20)
    p.pop()

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
