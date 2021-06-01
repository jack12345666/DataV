<template>
  <div id="dv-full-screen-container" :ref="ref">
    <template v-if="ready">
      <slot></slot>
    </template>
  </div>
</template>

<script>
import autoResize from '../../../mixin/autoResize.js'

export default {
  name: 'DvFullScreenContainer',
  mixins: [autoResize],
  data () {
    return {
      ref: 'full-screen-container',
      allWidth: 0,
      allHeight: 0,
      scale: 1,
      datavRoot: '',
      ready: false
    }
  },
  methods: {
    afterAutoResizeMixinInit () {
      const { initConfig, setAppScale } = this

      initConfig()

      setAppScale()

      this.ready = true
    },
    initConfig () {
      const { dom } = this
      this.allWidth = 1920
      this.allHeight = 1080
      dom.style.width = `1920px`
      dom.style.height = `1080px`
    },
    setAppScale () {
      const { allWidth, dom } = this

      const currentWidth = document.body.clientWidth
      dom.style.transform = `scale(${currentWidth / allWidth})`
      this.scale = currentWidth / allWidth
      dom.style.height = this.scale*1080 + 'px'
    },
    onResize () {
      const { setAppScale } = this

      setAppScale()
    }
  }
}
</script>