<template lang="pug">
  #app
    blocks(msg="Welcome to Your Vue.js App")
</template>

<script>
import Blocks from './components/Blocks.vue';

export default {
  name: 'app',
  components: {
    Blocks,
  },
};
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
</style>
