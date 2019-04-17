<template lang="pug">
  .blocks This is Blocks
    .blocks__buttons
      button(
        type='button'
        @click='addSimpleBlock') Add simple block
      button(
        type='button'
        @click='addNormalBlock') Add normal block
    .blocks__container
      .blocks__simple
        block(
          v-for='block in simpleBlocks'
          :id='block.id'
          :key='`simple-${block.id}`'
          type='simple'
          @close='closeBlock')
      .blocks__normal
        block(
          v-for='block in normalBlocks'
          :id='block.id'
          :key='`normal-${block.id}`'
          type='normal'
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

  data() {
    return {
      simpleBlocks: [],
      normalBlocks: [],
    };
  },

  methods: {
    addSimpleBlock() {
      this.simpleBlocks.push({ id: this.simpleBlocks.length });
    },

    addNormalBlock() {
      this.normalBlocks.push({ id: this.normalBlocks.length });
    },

    closeBlock(block) {
      if (block.type === 'simple') {
        const blockIndex = this.simpleBlocks.findIndex(index => (index.id === block.id));
        this.simpleBlocks.splice(blockIndex, 1);
      }
      if (block.type === 'normal') {
        const blockIndex = this.normalBlocks.findIndex(index => (index.id === block.id));
        this.normalBlocks.splice(blockIndex, 1);
      }
    },
  },
};
</script>

<style scoped lang="scss">
  .blocks {
    margin: 0 auto;
    max-width: 740px;

    &__buttons {
      display: flex;
      justify-content: space-evenly;
      padding-bottom: 50px;
    }

    &__buttons button {
      cursor: pointer;
      height: 30px;
      background: cornflowerblue;
      border: none;
      border-radius: 6px;
      width: 150px;
    }

    &__container {
      display: flex;
      justify-content: center;
    }

    &__simple, &__normal {
      display: flex;
      flex-direction: column;
      width: 250px;
    }
  }
</style>
