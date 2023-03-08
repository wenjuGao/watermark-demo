<template>
  <div class="card svg-mark">
    <div class="card-body">
      <h5 class="card-title">Svg做水印</h5>
      <p class="card-text">With supporting text below as a natural lead-in to additional content.</p>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue';
const createWaterMark = () => {
  const svgStr =
    `<svg xmlns="http://www.w3.org/2000/svg" width="180px" height="100px">
      <text x="0px" y="30px" dy="16px"
      text-anchor="start"
      stroke="#000"
      stroke-opacity="0.1"
      fill="none"
      transform="rotate(-20)"
      font-weight="100"
      font-size="16"
      >
      	前端小书童
      </text>
    </svg>`;
  return `data:image/svg+xml;base64,${window.btoa(unescape(encodeURIComponent(svgStr)))}`;
}
onMounted(() => {
  document.querySelector('.svg-mark').style.backgroundImage = `url(${createWaterMark()})`
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
