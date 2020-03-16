<template>
  <div class='sections limited'>
    <span v-if='false' class='center'>
      Tim is a science and technology enthusiast, researcher, writer, developer, research, and consultant. Jack of all trades, master of some. Unabashed generalist.
    </span>
    <span>
      <router-link class='grow' to='/dev'>
      <icon name='terminal' scale='4'></icon>
      <div style='text-align:center'>Web Dev</div>
      </router-link>
    </span>
    <span>
      <a class='grow' href='http://deepbreadth.io' target="_blank">
      <icon name='file-text' scale='4'></icon>
      <div style='text-align:center'>Writing</div>
      </a>
    </span>
    <span>
      <router-link class='grow' to='/photography'>
      <icon name='camera' scale='4' ></icon>
      <div style='text-align:center'>Photography</div>
      </router-link>
    </span>
    <span>
      <a class='grow' href='https://soundcloud.com/deep-breadth' target="_blank">
      <icon name='music' scale='4' ></icon>
      <div style='text-align:center'>Music</div>
      </a>
    </span>
  </div>
</template>
<script>
  import conf from '../config'

  export default {
    name: 'home',

    data () {
      return {
        lists: [],
        loading: true
      }
    },

    mounted () {
      window.document.title = conf.blogTitle + ' - home'
      // this.loadList()
    },

    methods: {
      loadList () {
        this.loading = true
      }
    }
  }
</script>
<style scoped>
.grow {
  transition: all .3s;
}
.grow:hover {
  transform: scale(1.2);
}
.sections {
  display: flex;
  flex-flow: row wrap;
  justify-content: space-around;
  font-weight: 100;
  font-size: 33px;
}
a {
  color: black
}
span a {
  width: 200px;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 40px;
}
</style>
