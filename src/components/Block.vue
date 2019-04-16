<template lang="pug">
  .blocks(:class='type')
    .blocks__close(@click='$emit("close")')
</template>

<script>
export default {
  name: 'Block',
  props: {
    type: { type: String, required: true },
  },
};
</script>

<style lang="scss" scoped>
    .blocks {
        height: 50px;
        width: 200px;
        position: relative;
        border: 1px solid #ccc;
        border-radius: 5px;

        &__close {
            color: #777;
            cursor: pointer;
            font: 14px/100% arial, sans-serif;
            position: absolute;
            right: 5px;
            text-decoration: none;
            text-shadow: 0 1px 0 #fff;
            top: 5px;
        }
        &__close:after {
            content: '✖';
        }
    }
</style>
