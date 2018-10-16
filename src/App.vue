<template>
  <div id="app">
    <highlight3 :selector="'#li-core-docs'" v-if="show"></highlight3>
    <!-- <highlight2 :selector="'#li-core-docs'" v-if="show"></highlight2> -->
    <!-- <highlight :selectors="'#li-core-docs'"></highlight> -->
    <img alt="Vue logo" src="./assets/logo.png" @click="showHighlight">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import Highlight from './highlight/indexZIndex'
import Highlight2 from './highlight/indexMutiDiv'
import Highlight3 from './highlight/indexCanvas'
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Highlight,
    Highlight2,
    Highlight3
  },
  data () {
    return {
      show: false
    }
  },
  methods: {
    showHighlight () {
      this.show = !this.show
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
