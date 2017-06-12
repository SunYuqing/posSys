<template>
  <div id="app">
    <left-nav></left-nav>
    <div class="main">
      <router-view></router-view>
    </div>

  </div>
</template>

<script>
  import leftNav from '@/components/common/leftNav';
  export default {
    name: 'app',
    components: {
      leftNav
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
html,body
  width: 100%
  height: 100%
#app
  display: flex
  font-family:'Microsoft YaHei', 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  overflow: hidden
  height: 100%
  width: 100%
  text-align: center
  color: #2c3e50
  .main
    flex: 1
    height: 100%
    overflow: hidden
    background: #f5f5ff

</style>
