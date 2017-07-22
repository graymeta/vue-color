<template>
  <div id="app">
    <a class="github-fork-ribbon" href="https://github.com/xiaokaike/vue-color" title="Fork me on GitHub">Fork me on GitHub</a>
    <div class="header-container">
      <div class="header-bg" :style="{'background-color': bgc}"></div>
      <header class="header">
        <div class="intro-wrap">
          <div class="intro">
            <h1>Vue-color</h1>
            <p>A Collection of Color Pickers from Sketch, Photoshop, Chrome, Github, Twitter, Material Design & more</p>
          </div>
        </div>
        <div class="demo-item">
          <chrome-picker :value="colors" @input="updateValue"></chrome-picker>
          <h6>Chrome</h6>
        </div>
      </header>
    </div>

    <div class="demo-container">
      <div class="demo-list">
        <div class="demo-item">
          <sketch-picker v-model="colors"></sketch-picker>
          <h6>Sketch</h6>
        </div>
        <div class="demo-item">
          <photoshop-picker v-model="colors" @ok="onOk" @cancel="onCancel"></photoshop-picker>
          <h6>Photoshop</h6>
        </div>
      </div>
      <div class="demo-list">
        <div class="demo-item">
          <material-picker v-model="colors"></material-picker>
          <h6>Material</h6>
        </div>
        <div class="demo-item">
          <slider-picker v-model="colors"></slider-picker>
          <h6>Slider</h6>
        </div>
      </div>
      <div class="demo-list">
        <div class="demo-item">
          <compact-picker v-model="colors" :default-colors="compactColors"></compact-picker>
          <h6>Compact</h6>
        </div>
        <div class="demo-item">
          <swatches-picker v-model="colors"></swatches-picker>
          <h6>Swatches</h6>
        </div>
      </div>


    </div>
  </div>
</template>

<script>
import material from '../src/components/Material.vue'
import compact from '../src/components/Compact.vue'
import swatches from '../src/components/Swatches.vue'
import slider from '../src/components/Slider.vue'
import sketch from '../src/components/Sketch.vue'
import chrome from '../src/components/Chrome.vue'
import photoshop from '../src/components/Photoshop.vue'

let defaultProps = {
  hex: '#194d33',
  hsl: {
    h: 150,
    s: 0.5,
    l: 0.2,
    a: 1
  },
  hsv: {
    h: 150,
    s: 0.66,
    v: 0.30,
    a: 1
  },
  rgba: {
    r: 25,
    g: 77,
    b: 51,
    a: 1
  },
  a: 1
}

const defaultColors = [
  '#FFC107', '#FF9800', '#FF5722', '#E91E63', '#9C27B0', '#673AB7', '#3F51B5', '#2196F3', '#0097A7', '#009688', '#4CAF50', '#AFB42B', '#795548', '#607D8B',
  '#FFD54F', '#FFB74D', '#FF8A65', '#E57373', '#BA68C8', '#9575CD', '#7986CB', '#4FC3F7', '#4DD0E1', '#4DB6AC', '#81C784', '#DCE775', '#A1887F', '#90A4AE',
  '#FFECB3', '#FFE0B2', '#FFCCBC', '#FFCDD2', '#E1BEE7', '#D1C4E9', '#C5CAE9', '#B3E5FC', '#B2EBF2', '#B2DFDB', '#DCEDC8', '#F0F4C3', '#D7CCC8', '#CFD8DC'
]
const compactColors = defaultColors.map(c => {
  return { hex: c, disabled: false }
})
for (let i = 0; i < defaultColors.length; i += 3) {
  compactColors[i].disabled = true
}

export default {
  components: {
    'material-picker': material,
    'compact-picker': compact,
    'swatches-picker': swatches,
    'slider-picker': slider,
    'sketch-picker': sketch,
    'chrome-picker': chrome,
    'photoshop-picker': photoshop
  },
  data () {
    return {
      colors: defaultProps,
      compactColors: compactColors
    }
  },
  computed: {
    bgc () {
      return this.colors.hex
    }
  },
  methods: {
    onOk () {
      console.log('ok')
    },
    onCancel () {
      console.log('cancel')
    },
    updateValue (value) {
      this.colors = value
    }
  },
  created () {
  }
}
</script>

<style lang="stylus">
*
  margin 0
  padding 0
html
  font-family 'Source Sans Pro', 'Helvetica Neue', Arial, sans-serif
.header-container
  position relative
  .header-bg
    position absolute
    top 0
    left 0
    right 0
    min-height 580px
    background-color #333
    opacity 0.5
    z-index 0
  .header
    display flex
    max-width 780px
    margin 0 auto
    padding 20px 0
    .intro-wrap
      flex 1
      margin-right 100px
    .intro
      width 300px
      color rgba(0, 0, 0, 0.65098)
      > h1
        font-size 40px
        font-weight normal
        line-height 60px
      > p
        font-size 16px
        font-weight normal
        line-height 22px

.demo-container
  max-width 780px
  min-height 800px
  margin 0 auto
  position relative
  z-index 2
  .demo-list
    display flex
    margin-bottom 20px
.demo-item
  position relative
  margin-bottom 10px
  margin 0 10px 0 10px
  z-index 2
  h6
    margin 0
    padding 5px 0
    color #666

</style>
