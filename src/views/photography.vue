<template>
<div @keyup.left="test">
  <transition name='fade'>
  <div id='box' v-if="focused" @click='focused=false'>
    <transition name='fade' >
      <img @click.stop.prevent='' v-if='focusURL' :src="focusURL" />
    </transition>
  </div>
  </transition>
  <isotope :class="{'blur':focused}" id='photos' ref='photo' :options='{}' :list="images" >
    <img @click="focus(k)" class='item lazyfade' v-for="element, k in images" :key="element.src" v-lazy="'/static/' + element.src" />
  </isotope>
</div>
</template>

<style scoped>
#box {
  z-index: 2;
  position: fixed;
  height: 100vh;
  width: 100vw;
  background-color: #00000099;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.blur {
  filter: blur(5px)!important;
}
#box img {
  max-height: 100%;
  max-width: 100%;
  height: auto;
  width: auto;
  display: block;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  box-sizing: border-box;
  margin: auto;
}
img[lazy=loading] {
width: 30px!important;
margin: calc(15% - 30px);
opacity: 1;
height: 30px;
 }
.lazyfade[lazy=loaded]{
  opacity: 1!important;
}
#photos {
  transition: filter 1s linear;
  filter: blur(0);
}
#photos img {
  width: calc(33% - 10px);
  /* height: auto !important; */
  padding: 5px;
  opacity: 0;
  transition: opacity 2s;
}
@media (max-width: 800px) {
  #photos img {
  width: calc(50% - 10px);
  }
}
@media (max-width: 400px) {
  #photos img {
    width: calc(100% - 10px);
  }
}

</style>

<script>
import conf from '../config'
import {images} from '../utils/gallery'
import isotope from 'vueisotope'

export default {

  components: {
    isotope
  },

  name: 'photography',

  data () {
    return {
      title: 'photography - ' + conf.blogTitle,
      images: images,
      focusURL: '',
      focused: false,
      focusedIndex: undefined
    }
  },

  methods: {
    focus (index) {
      this.focusURL = ''
      this.$nextTick(() => { // hack to use enter/leave fade transition on image
        this.focusURL = 'static/' + this.images[index].src
        this.focused = true
        this.focusIndex = index
      })
    }
  },

  mounted () {
    window.setInterval(() => {
      this.$refs.photo.layout('masonry')
    }, 300)
    document.addEventListener('keydown', (e) => { // escape
      if (e.keyCode === 27) {
        this.focused = false
      }
    })
    document.addEventListener('keydown', (e) => { // left
      if (e.keyCode === 37) {
        this.focus(this.focusIndex - 1)
      }
    })
    document.addEventListener('keydown', (e) => { // right
      if (e.keyCode === 39) {
        this.focus(this.focusIndex + 1)
      }
    })
  }
}
</script>
