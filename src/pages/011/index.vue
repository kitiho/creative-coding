<route lang="yaml">
name: 並べる
meta: 
  order: 11
</route>
<script setup lang="ts">
import P5 from 'p5'
import { onMounted, ref } from 'vue';
function init() {
  new P5(sketch)
  new P5(sketch2)
  new P5(sketch3)
}

function sketch(p: P5) {
  p.setup = () => {
    const canvas = p.createCanvas(400, 400)
    canvas.style('margin', '16px')
    canvas.parent('#container')
    p.background(103, 107, 121)

    f(2, p.height / 3)
    f(7, p.height / 3 * 2)

  }
  p.windowResized = () => {

    p.resizeCanvas(p.windowWidth, p.windowHeight)
  }
  function f(n, ty) {
    p.push()
    p.stroke(240)
    p.noFill()
    p.line(0, ty, p.width, ty)
    p.pop()

    for (let i = 0; i < n; i++) {
      const tx = p.width / (n - 1) * i
      p.circle(tx, ty, 30)
    }
  }
}
function sketch2(p: P5) {
  p.setup = () => {
    const canvas = p.createCanvas(400, 400)
    canvas.style('margin', '16px')
    canvas.parent('#container')
    p.background(103, 107, 121)

    const n = 10
    for (let y = 0; y < n; y++) {
      for (let x = 0; x < n; x++) {
        const tx = p.width / (n - 1) * x
        const ty = p.height / (n - 1) * y
        p.circle(tx, ty, 30)
      }
    }

  }
  p.windowResized = () => {
    p.resizeCanvas(p.windowWidth, p.windowHeight)
  }
}

function sketch3(p: P5) {
  p.setup = () => {
    const canvas = p.createCanvas(400, 400)
    canvas.style('margin', '16px')
    canvas.parent('#container')
    p.background(103, 107, 121)

    const n = 5;
    const w = p.width / n;
    const h = p.height / n;
    for (let y = 0; y < n; y++) {
      for (let x = 0; x < n; x++) {
        drawCircle(x * w, y * h, w, h)
      }
    }
  }
  p.windowResized = () => {
    p.resizeCanvas(p.windowWidth, p.windowHeight)
  }
  function drawCircle(x, y, w, h) {
    p.translate(x, y)
    p.circle(w / 2, h / 2, 30)
    p.resetMatrix()
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
