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
      scale: 0,
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
    //   const { width, height } = window.screen
      const width = document.documentElement.clientWidth || document.body.clientWidth
      const height = document.documentElement.clientHeight || document.body.clientHeight 
      
      this.allHeight = height
      this.allWidth = width

      dom.style.width = `${width}px`
      dom.style.height = `${height}px`
    },
    setAppScale () {
      const { allWidth, allHeight, dom } = this

      const currentWidth = document.body.clientWidth
      const currentHeight = document.body.clientHeight

      dom.style.transform = `scale(${currentWidth / allWidth}, ${currentHeight / allHeight})`
    },
    onResize () {
      const { setAppScale } = this

      setAppScale()
    }
  }
}
</script>
