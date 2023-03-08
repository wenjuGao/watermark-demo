<template>
  <div class="card canvas-images-watermark-wrapper">
    <div class="card-body">
      <h5 class="card-title">Canvas写入图片做背景水印</h5>
      <p class="card-text">With supporting text below as a natural lead-in to additional content.</p>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue';
import ImageBg from "../assets/bg.png"
const createWaterMark = ({
  width = 120,
  height = 120,
}) => {
  const canvas = document.createElement('canvas');
  canvas.width = width;
  canvas.height = height;
  return {
    canvas,
    ctx: canvas.getContext('2d')
  };
}
onMounted(() => {
  const img = new Image();
  const { ctx, canvas } = createWaterMark({});
  img.onload = function () {
    ctx.globalAlpha = 0.2;
    ctx.rotate(Math.PI / 180 * 20);
    // 获取指定区域的canvas像素信息
    ctx.drawImage(img, 0, 16, 180, 100);
    document.querySelector(".canvas-images-watermark-wrapper").style.backgroundImage = `url(${canvas.toDataURL()})`
  };
  img.src = ImageBg
});

</script>

<style scoped></style>
