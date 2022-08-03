<route lang="yaml">
name: 画像とレイアウト
meta: 
  order: 9
</route>
<script setup lang="ts">
import P5 from 'p5'
import { onMounted, ref } from 'vue';
function init() {
  new P5(sketch)
  new P5(sketch2)
}

function sketch(p: P5) {
  let img
  p.preload = () => {
    img = p.loadImage(new URL('../../assets/image.png', import.meta.url).href)

  }
  p.setup = () => {
    const canvas = p.createCanvas(400, 400)
    canvas.style('margin', '16px')
    canvas.parent('#container')
    p.background(103, 107, 121)
    const a = p.width / p.height
    const b = img.width / img.height
    let w = 0, h = 0
    if (a < b) {
      w = p.width
      h = img.height * w / img.width
    } else {
      h = p.height
      w = img.width * h / img.height
    }

    p.noSmooth()
    p.image(img, (p.width - w) / 2, (p.height - h) / 2, w, h)
  }
  p.windowResized = () => {
    p.resizeCanvas(p.windowWidth, p.windowHeight)
  }
}
function sketch2(p: P5) {
  let img;
  const cw = 16;
  const ch = 18;
  const scale = 5;
  p.preload = () => {
    img = p.loadImage(new URL('../../assets/copy.png', import.meta.url).href)
  }
  p.setup = () => {
    const canvas = p.createCanvas(400, 400)
    canvas.style('margin', '16px')
    canvas.parent('#container')
    p.background(103, 107, 121)

    p.noSmooth()
    for (let i = 0; i < 3; i++) {
      p.copy(img, cw * i, 0, cw, ch, cw * i * scale, 0, cw * scale, ch * scale)
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
