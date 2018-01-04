<style>
  [vswipe] {
    overflow: hidden;
    visibility: hidden;
    position: relative;
  }
  .swipe-wrap {
    overflow: hidden;
    position: relative;
  }
</style>
<template>
  <div vswipe>
    <div class='swipe-wrap'>
      <slot></slot>
    </div>
  </div>
</template>
<script>
  import Swipe from 'swipe-js-iso'

  function noop () {}

  export default {
    props: {
      options: {
        startSlide: { type: Number, default: 0 },
        speed: { type: Number, default: 400 },
        auto: { type: Number, default: 3000 },
        continuous: { type: Boolean, default: true },
        disableScroll: { type: Boolean, default: false },
        stopPropagation: { type: Boolean, default: false },
        callback: { type: Function, default: noop },
        transitionEnd: { type: Function, default: noop }
      }
    },

    data () {
      return {
        swipe: undefined
      }
    },

    mounted () {
      this.swipe = new Swipe(this.$el, this.options)
    },

    destroyed () {
      this.swipe.kill()
    },

    methods: {
      prev (restart) {
        this.swipe.prev(restart)
      },

      next (restart) {
        this.swipe.next(restart)
      },

      getPos () {
        return this.swipe.getPos()
      },

      getNumSlides () {
        return this.swipe.getNumSlides()
      },

      slide (index, duration) {
        this.swipe.slide(index, duration)
      },

      resize () {
        setTimeout(this.swipe.setup, 0)
      }
    }
  }
</script>
