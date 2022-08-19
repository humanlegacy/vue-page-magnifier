<template>
  <div class="magnifier-container" ref="container">
    <!-- 页面原始内容 -->
    <slot></slot>

    <div class="magnifier" :style="{width:width,height:height}" ref="magnifier">
      <div class="magnifier-lens"></div>
      <!-- 镜像内容 -->
      <div class="magnifier-shadow" ref="shadow"><slot></slot></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    scale: {
      type: Number,
      default: 2
    },
    width: {
      type: String,
      default: '150px'
    },
    height: {
      type: String,
      default: '150px'
    }
  },
  mounted() {
    var magnifier = this.$refs.magnifier
    var magnifierContainer = this.$refs.container
    var shadow = this.$refs.shadow
    shadow.style.width = magnifierContainer.clientWidth + 'px'

    document.addEventListener('scroll', () => {
      const scrollHigh = document.documentElement.scrollTop || document.body.scrollTop
      shadow.style.top = parseInt(shadow.style.top) - scrollHigh * this.scale + 'px'
    })

    document.addEventListener('mousemove', (e) => {
      magnifier.style.left = e.clientX - magnifier.clientWidth / 2 + 'px'
      magnifier.style.top = e.clientY - magnifier.clientHeight / 2 + 'px'

      const scrollHigh = document.documentElement.scrollTop || document.body.scrollTop
      shadow.style.transform = 'scale(' + this.scale + ')'
      shadow.style.top = (magnifierContainer.offsetTop - e.clientY) * this.scale + magnifier.clientHeight / 2 - scrollHigh * this.scale + 'px'
      shadow.style.left = (magnifierContainer.offsetLeft - e.clientX) * this.scale + magnifier.clientWidth / 2 + 'px'
    }, false)

  }
}
</script>

<style scoped>
.magnifier-container {
  width: 100%;
}
.magnifier {
  position: fixed;
  z-index: 999;
  border-radius: 50%;
  outline: 5px solid #000;
  box-shadow: 0 0 50px rgba(0, 0, 0, 0.9);
  background: #fff;
  overflow: hidden !important;
}

.magnifier-lens {
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  z-index: 100;
  position: absolute;
  cursor: none;
}
.magnifier-shadow {
  transform-origin: 0px 0px;
  position: absolute;
}
</style>
