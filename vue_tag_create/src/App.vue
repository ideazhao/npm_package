<template>
  <div id="app">
    <vue-tag-create></vue-tag-create>
  </div>
</template>

<script>
import VueTagCreate from "./component"
export default {
  name: 'app',
  data () {
    return {
    }
  },
  components:{
    VueTagCreate
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
html,body{
  font-size: 10px;
}
</style>
