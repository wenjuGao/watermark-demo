<template>
  <div class="card shadow-watermark"
       ref="shadowRef">
    <div class="card-body">
      <h5 class="card-title">shadowDom水印</h5>
      <p class="card-text">With supporting text below as a natural lead-in to additional content.</p>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
const shadowRef = ref()
class ShadowMark extends HTMLElement {
  constructor() {
    super();
    const shadowRoot = this.attachShadow({ mode: 'open' });
    const wrapContainer = document.createElement('div')
    const style = document.createElement('style');
    style.textContent = `
			.wrapContainer {
				width: 100%;
				height: 100%;
				display: flex;
				flex-wrap: wrap;
        position: absolute;
        top: 0;
        left: 0;
			}
			.watermark-item {
				display: flex;
				font-size: 16px;
				opacity: .3;
				transform: rotate(-20deg);
				user-select: none;
				white-space: nowrap;
				justify-content: center;
				align-items: center;
			}`;
    const waterHeight = 100
    const waterWidth = 100
    const { clientWidth, clientHeight } = document.querySelector('.shadow-watermark')
    const column = Math.ceil(clientWidth / waterWidth)
    const rows = Math.ceil(clientHeight / waterHeight)
    wrapContainer.setAttribute('class', "wrapContainer")
    for (let i = 0; i < column * rows; i++) {
      const wrap = document.createElement('div')
      wrap.setAttribute('class', 'watermark-item')
      wrap.style.width = waterWidth + 'px'
      wrap.style.height = waterHeight + 'px'
      wrap.textContent = "前端小书童"
      wrapContainer.appendChild(wrap)
    }
    shadowRoot.appendChild(style);
    shadowRoot.appendChild(wrapContainer)
  }
}
onMounted(() => {
  customElements.define('shadow-mark', ShadowMark);
  shadowRef.value.appendChild(new ShadowMark())
});

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less" scoped>
.card {
  position: relative;
  overflow: hidden;
  background-color: transparent;

  .mark {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    flex-wrap: wrap;
  }
}
</style>
