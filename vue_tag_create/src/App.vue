<template>
  <div id="app">
    <vue-tag-create :limit='20' :iconClass="iconClass" :inline="true" :placeholder="placeholder"></vue-tag-create>
  </div>
</template>

<script>
import VueTagCreate from "./component"
export default {
  name: 'app',
  data () {
    return {
      iconClass:'iconfont icon-close',
      placeholder:'请输入不超过20个字的标签'
    }
  },
  components:{
    VueTagCreate
  }
}
</script>

<style lang="scss">
#app {
  margin-top: 60px;
}
html,body{
  font-size: 10px;
}
</style>