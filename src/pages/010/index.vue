<route lang="yaml">
name: 座標変換
meta: 
  order: 10
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
  let s = 0;
  p.setup = () => {
    const canvas = p.createCanvas(400, 400)
    canvas.style('margin', '16px')
    canvas.parent('#container')
    p.background(103, 107, 121)

    s = 1
  }
  p.draw = () => {
    p.clear(0, 0, 0, 0);
    p.background(103, 107, 121)

    p.translate(p.width / 2, p.height / 2)
    p.scale(s, s)
    p.circle(0, 0, 10)
    p.resetMatrix()
    s += 0.1

  }
  p.windowResized = () => {
    p.resizeCanvas(p.windowWidth, p.windowHeight)
  }
}
function sketch2(p: P5) {
  let r;
  p.setup = () => {
    const canvas = p.createCanvas(400, 400)
    canvas.style('margin', '16px')
    canvas.parent('#container')
    p.background(103, 107, 121)
    r = 0;
  }
  p.draw = () => {
    p.clear(0, 0, 0, 0);
    p.background(103, 107, 121)

    p.translate(p.width / 2, p.height / 2)
    p.rotate(r)
    p.rect(-50, -50, 100, 100)
    p.resetMatrix()
    drawMarker(p.width / 2, p.height / 2)

    r += 0.01;
  }
  p.windowResized = () => {
    p.resizeCanvas(p.windowWidth, p.windowHeight)
  }

  function drawMarker(x, y) {
    p.line(x - 10, y, x + 10, y)
    p.line(x, y - 10, x, y + 10)
  }
}

function sketch3(p: P5) {
  const n = 20;
  let s = 0.9;
  let a;
  p.setup = () => {
    const canvas = p.createCanvas(400, 400)
    canvas.style('margin', '16px')
    canvas.parent('#container')
    p.background(103, 107, 121)

    p.angleMode(p.DEGREES)
    p.rectMode(p.CENTER)
    p.colorMode(p.HSB)
    p.strokeWeight(4)
    a = 0
  }
  p.draw = () => {
    p.clear(0, 0, 0, 0);
    p.colorMode(p.RGB)
    p.background(103, 107, 121)

    p.colorMode(p.HSB)
    p.translate(p.width / 2, p.height / 2)
    for (let i = 0; i < n; i++) {
      p.scale(s)
      p.rotate(a)
      p.fill(i * 20, 100, 100)
      p.rect(0, 0, 200, 200)
    }
    a += 0.1
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
