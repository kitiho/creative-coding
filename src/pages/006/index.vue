<route lang="yaml">
name: 正規化・線形補間・マップ
meta: 
  order: 6
</route>
<script setup lang="ts">
import P5 from 'p5'
import { onMounted, ref } from 'vue';
import { $ref } from 'vue/macros'
const container = ref()
function init() {
  new P5(sketch, container.value)
}
function sketch(p: P5) {
  let x: number, x1: number, x2: number, y: number
  let a, b, t, i, rt
  let space = 20
  const route = [
    { x: 100, y: 100 },
    { x: 300, y: 300 },
    { x: 300, y: 100 },
  ];

  p.setup = () => {
    p.createCanvas(p.windowWidth, p.windowHeight)
    x1 = 30;
    x2 = p.width - 30;
    x = x1;
    y = p.height / 2;

    a = { x: space, y: space }
    b = { x: p.width - space, y: p.height - space }
    p.textAlign(p.CENTER, p.CENTER)
    t = 0
    i = 0;
    rt = 0
  }
  p.draw = () => {
    p.clear(0, 0, 0, 0)
    x = x + 1
    if (x >= x2) {
      x = x1
    }
    p.noStroke()
    p.fill(240)
    p.text(x1, x1, y - 65);
    p.text(x2, x2, y - 65);
    p.text(x, x, y - 65);
    p.text(p.norm(x, x1, x2).toFixed(2), x, y + 65);
    p.text(0, x1, y + 65);
    p.text(1, x2, y + 65);

    p.stroke(240);
    p.noFill();
    p.line(x1, y - 45, x1, y - 25);
    p.line(x2, y - 45, x2, y - 25);
    p.line(x, y - 45, x, y - 25);
    p.line(x, y + 45, x, y + 25);
    p.line(x1, y + 45, x1, y + 25);
    p.line(x2, y + 45, x2, y + 25);

    p.stroke(240);
    p.noFill();
    p.line(x1, y, x2, y);

    p.stroke(240);
    p.fill("#292a33");
    p.circle(x, y, 20);

    t += 0.001
    t = t % 1

    p.stroke(240);
    p.noFill()
    p.line(a.x, a.y, b.x, b.y)
    p.fill('#292a33')
    p.circle(p.lerp(a.x, b.x, t), p.lerp(a.y, b.y, t), 20)

    p.fill(240)
    p.text("t = " + t.toFixed(2), p.width / 2, space * 2);
    p.text("a", space, space * 2);
    p.text("b", p.width - space, p.height - space * 2);

    route.forEach(r => {
      p.circle(r.x, r.y, 20)
    })

    const prev = route[i]
    const next = route[(i + 1) % route.length]
    const rx = p.lerp(prev.x, next.x, rt)
    const ry = p.lerp(prev.y, next.y, rt)
    p.circle(rx, ry, 20)
    rt += 0.01
    if (rt > 1) {
      rt = 0
      i++
      i = i % route.length
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
  <div ref="container" id="canvas" />
</template>

<style scoped>
#canvas {
  background: #292a33;
  overflow: hidden;
}
</style>
