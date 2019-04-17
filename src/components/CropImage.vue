<template>
  <div>
    <canvas ref="canvas"></canvas>
  </div>
</template>
<script>
export default {
  name: 'CropImage',
  props: {
    cWidth: {
      type: Number,
      default: 120
    },
    cHeight: {
      type: Number,
      default: 50
    },
    imgUrl: String
  },
  data () {
    return {
    }
  },
  created () {
  },
  mounted () {
    let canvas = this.$refs.canvas
    let cWidth = this.cWidth
    let cHeight = this.cHeight
    let imgUrl = this.imgUrl
    this.canvasImage(canvas, cWidth, cHeight, imgUrl)
  },
  methods: {
    canvasImage (canvasEl, cWidth, cHeight, imgUrl) {
      let ctx = canvasEl.getContext('2d')
      let img = new Image()
      this.convertToBlod(imgUrl).then((blob) => {
        img.src = URL.createObjectURL(blob)
        img.onload = function () {
          canvasEl.width = cWidth
          canvasEl.height = cHeight
          let w = img.width
          let h = img.height
          // dw dh 按小者裁剪
          let dw = w / cWidth
          let dh = h / cHeight
          let sx = 0
          let sy = 0
          let sw = 0
          let sh = 0
          if (dw > dh) {
            sh = h
            sw = cWidth * dh
            sx = parseInt((w - cWidth * dh) / 2)
          } else {
            sw = w
            sh = cHeight * dw
            sy = parseInt((h - cHeight * dw) / 2)
          }
          ctx.drawImage(img, sx, sy, sw, sh, 0, 0, cWidth, cHeight)
          URL.revokeObjectURL(img.src)
        }
      })
    },
    convertToBlod (url) {
      return new Promise(resolve => {
        const xhr = new XMLHttpRequest()
        xhr.open('GET', url, true)
        xhr.responseType = 'blob'
        xhr.onload = () => {
          if (xhr.status === 200) {
            resolve(xhr.response)
          }
        }
        xhr.send()
      })
    }
  }
}
</script>
<style scoped lang="scss">
</style>
