<template lang="pug">
  .blocks This is Blocks
    block(
      type='simple'
      @close='closeBlock')
</template>

<script>
import Block from './Block.vue';

export default {
  name: 'Blocks',

  components: {
    Block,
  },

  props: {
    msg: String,
  },

  methods: {
    closeBlock() {
      console.log('closed');
    },
  },
};
</script>

<style scoped lang="scss">

</style>
