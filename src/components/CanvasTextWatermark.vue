<template>
  <div class="card canvas-text">
    <div class="card-body">
      <h5 class="card-title">Canvas写入文字做背景水印</h5>
      <p class="card-text">With supporting text below as a natural lead-in to additional content.</p>
    </div>
  </div>
</template>


<script setup>
import { onMounted } from 'vue';
const createWaterMark = ({
  rotate = -20,
  text = '',
  width = 100,
  height = 100,
  fillStyle = '#000',
  opacity = 0.2,
  font = `16px serif`
}) => {
  const canvas = document.createElement('canvas');
  canvas.width = width;
  canvas.height = height;
  const ctx = canvas.getContext('2d');
  ctx.clearRect(0, 0, width, height);
  ctx.fillStyle = fillStyle;
  ctx.globalAlpha = opacity;
  ctx.font = font
  ctx.rotate(Math.PI / 180 * rotate);
  ctx.fillText(text, 0, 50);
  return canvas.toDataURL();
}
onMounted(() => {
  document.querySelector(".canvas-text").style.backgroundImage = `url(${createWaterMark({ text: "前端小书童" })})`
});

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
