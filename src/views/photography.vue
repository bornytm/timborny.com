<template>
<div>
  <isotope id='photos' ref='photo' :options='{}' :list="images" >
    <img class='item lazyfade' v-for="element in images" :key="element.src" v-lazy="'/static/' + element.src" />
  </isotope>
</div>
</template>

<style scoped>
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
}
#photos img {
  width: calc(33% - 10px);
  /* height: auto !important; */
  padding: 5px;
  /* opacity: 0; */
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
      images: images
    }
  },
  mounted () {
    window.setInterval(() => {
      console.log('hi')
      this.$refs.photo.layout('masonry')
    }, 100)
  }
}
</script>
