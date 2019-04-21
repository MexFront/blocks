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
          @close='closeBlock'
          @highlight='highlightToggle')
      .blocks__normal
        block(
          v-for='block in normalBlocks'
          :id='block.id'
          :key='`normal-${block.id}`'
          type='normal'
          @styled='setStyleNum'
          @switched='setSwitchedNum'
          @close='closeBlock'
          @highlight='highlightToggle')
    info.blocks__info(
      :green='green'
      :highlighted='highlighted'
      :red='red'
      :total='blocksTotal')
</template>

<script>
import Block from './Block.vue';
import Info from './Info.vue';

export default {
  name: 'Blocks',

  components: {
    Block,
    Info,
  },

  props: {
    msg: String,
  },

  data() {
    return {
      blocksTotal: 0,
      green: 0,
      highlighted: 0,
      red: 0,
      simpleBlocks: [],
      normalBlocks: [],
    };
  },

  methods: {
    addSimpleBlock() {
      this.simpleBlocks.push({ id: this.simpleBlocks.length + 1 });
      this.blocksTotal += 1;
    },

    addNormalBlock() {
      this.normalBlocks.push({ id: this.normalBlocks.length + 1 });
      this.blocksTotal += 1;
    },

    closeBlock(block) {
      if (block.type === 'simple') {
        const blockIndex = this.simpleBlocks.findIndex(index => (index.id === block.id));
        this.simpleBlocks.splice(blockIndex, 1);
        this.blocksTotal -= 1;
      }
      if (block.type === 'normal') {
        if (block.el.contains('_green')) this.green -= 1;
        if (block.el.contains('_red')) this.red -= 1;
        const blockIndex = this.normalBlocks.findIndex(index => (index.id === block.id));
        this.normalBlocks.splice(blockIndex, 1);
        this.blocksTotal -= 1;
      }
    },

    highlightToggle(status) {
      if (status === 'true') this.highlighted += 1;
      else this.highlighted -= 1;
    },

    setStyleNum(val) {
      if (val === '_green') this.green += 1;
      if (val === '_red') this.red += 1;
    },

    setSwitchedNum(val) {
      if (val === '_green') {
        this.green += 1;
        this.red -= 1;
      }
      if (val === '_red') {
        this.green -= 1;
        this.red += 1;
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
      justify-content: center;
      padding-bottom: 50px;
    }

    &__buttons button {
      cursor: pointer;
      height: 30px;
      background: cornflowerblue;
      border: none;
      border-radius: 6px;
      margin: 0 10px;
      width: 220px;
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

    &__info {
      position: absolute;
      bottom: 100px;
      left: 44%;
    }
  }
</style>
