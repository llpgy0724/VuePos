<template>
  <div id="app">
    <Left></Left>
    <Middle></Middle>
  </div>
</template>

<script>
import Left from '@/components/left.vue'
import Middle from '@/components/middle.vue'

export default {
  name: 'app',
  components: {
    Left,
    Middle
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
html,body,#app{
  height: 100%;
  padding: 0;
  margin: 0;
}
ul{
  list-style-type: none;
}
</style>
