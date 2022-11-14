<template>
  <div id="app">
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <Post/>
    
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Post from "./components/common/Post.vue"


export default {
  name: 'App',
  components: {
    HelloWorld, Post
  },
  data() {
    return {
      
      
    }
  },
  
  methods: {
    
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}


</style>
