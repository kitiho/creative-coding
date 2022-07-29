<route lang="yaml">
name: イージング
meta: 
  order: 8
</route>
<script setup lang="ts">
import P5 from 'p5'
import { onMounted, ref } from 'vue';
const container = ref()
function init() {
  new P5(sketch)
  new P5(sketch2)
}

function sketch(p: P5) {
  let t = 0;
  let x1, y1, x2, y2;
  p.setup = () => {
    const canvas = p.createCanvas(400, 400)
    canvas.style('margin', '16px')
    canvas.parent('#canvas')
    x1 = 0;
    y1 = p.height;
    x2 = p.width;
    y2 = 0;
    t = 0;
  }
  p.draw = () => {
    p.clear(0, 0, 0, 0);
    p.background(103, 107, 121)
    const x = p.lerp(x1, x2, tt(t))
    const y = p.lerp(y1, y2, tt(t));
    t += 0.005;
    if (t > 1) {
      t = 0;
    }
    p.circle(x, y, 20);
  }
  p.windowResized = () => {

    p.resizeCanvas(p.windowWidth, p.windowHeight)
  }
}

function sketch2(p: P5) {
  let prevR = 0, nextR = 0, d = 0, t = 0;
  function reset() {
    prevR = d;
    nextR = p.random(20, 400);
    t = 0;
  }
  p.setup = () => {
    const canvas = p.createCanvas(400, 400)
    canvas.style('margin', '16px')
    canvas.parent('#canvas')
    reset();
    d = 200;
  }
  p.draw = () => {

    t += 0.01;
    if (t >= 1.4) {
      reset();
      return;
    }
    if (t > 1.0) {
      return;
    }
    p.clear(0, 0, 0, 0);
    p.background(103, 107, 121)

    d = p.lerp(prevR, nextR, easeInOutBack(t));
    p.circle(p.width / 2, p.height / 2, d);
  }
  p.windowResized = () => {

    p.resizeCanvas(p.windowWidth, p.windowHeight)
  }

}
function easeInOutBack(t) {
  const c1 = 1.70158;
  const c2 = c1 * 1.525;

  return t < 0.5 ? (Math.pow(2 * t, 2) * ((c2 + 1) * 2 * t - c2)) / 2 : (Math.pow(2 * t - 2, 2) * ((c2 + 1) * (t * 2 - 2) + c2) + 2) / 2;
}
function tt(t) {
  return t * t;
}
onMounted(() => {
  init()
})
</script>
<template>
  <div ref="container" id="canvas" />
</template>

<style scoped >
#canvas {
  width: 100%;
  height: 100%;
  background: #292a33;
  overflow: hidden;
}
</style>
