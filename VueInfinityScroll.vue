<template>
  <div>
    <div
      :height="height"
      :class="visClass"
      :style="defaultStyle"
      :buttonText="buttonText"
      :resetScroll="resetScroll"
      :hasNextPage="hasNextPage"
      :visSmallScreen="visSmallScreen"
      :visLargeScreen="visLargeScreen"
      :visMidScreen="visMidScreen"
      :visAllScreen="visAllScreen"
      :buttonClass="buttonClass"
      :buttonIcon="buttonIcon"
      @scroll="onScroll">
      <slot></slot>
      <button @click.prevent="toTop" class="to-top" :class="buttonClass" title="Ir ao Topo">
        <i :class="buttonIcon" /> {{ buttonText }}
      </button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    visClass: {
      type: String
    },
    visHeight: {
      type: String
    },
    hasNextPage: {
      type: Boolean,
      required: true
    },
    resetScroll: {
      type: Boolean,
      default: false
    },
    buttonClass: {
      type: String,
      default: ''
    },
    buttonText: {
      type: String,
      default: 'Go to top'
    },
    visSmallScreen: {
      type: String,
      default: ''
    },
    visLargeScreen: {
      type: String,
      default: ''
    },
    visMidScreen: {
      type: String,
      default: ''
    },
    visAllScreen: {
      type: String,
      default: ''
    },
    buttonIcon: {
      type: String,
      default: ''
    }
  },
  name: 'vue-infinity-scroll',
  data () {
    return {
      defaultStyle: 'height: 50vh; overflow-y: scroll',
      height: ''
    }
  },
  mounted () {
    this.onScroll()
    this.getWindowHeight()
    this.$nextTick(() => {
      window.addEventListener('resize', this.getWindowHeight)
      this.getWindowHeight()
    })
  },
  methods: {
    onScroll () {
      let element = this.$el.querySelector('div')
      const el = this.$el.querySelector('.to-top')
      element.scrollTop > 150 ? el.style.display = 'block' : el.style.display = 'none'
      let end = element.scrollHeight - element.scrollTop === element.clientHeight
      if (end && this.hasNextPage) {
        this.$emit('scrolling')
      }
    },

    toTop () {
      this.$el.querySelector('div').scrollTop = 0
    },

    getWindowHeight (event) {
      let windowHeight = document.documentElement.clientHeight
      if (windowHeight < 1000 && windowHeight > 768) {
        this.visAllScreen.length ? this.height = this.visAllScreen : this.height = this.visMidScreen
      } else if (windowHeight < 768) {
        this.visAllScreen.length ? this.height = this.visAllScreen : this.height = this.visSmallScreen
      } else {
        this.visAllScreen.length ? this.height = this.visAllScreen : this.height = this.visLargeScreen
      }
    }
  },
  watch: {
    height (vl) {
      this.defaultStyle = `height: ${vl}; overflow-y: scroll;`
    },

    resetScroll (vl) {
      if (!vl) return
      this.toTop()
    }
  }
}
</script>

<style scoped lang="css">
.to-top {
  display: none;
  position: absolute;
  bottom: 20px;
  right: 25px;
  z-index: 99;
  border: none;
  outline: none;
  color: white;
  cursor: pointer;
  border-radius: 5px;
}
</style>
