<template lang="pug">
  .block(
    :class='[isStyleNormal, { _highlighted: highlighted }]'
    @click='highlight'
    @dblclick='changeStyle') I am {{ type }} block # {{ id }}
    .block__close(@click='close')
</template>

<script>
export default {
  name: 'Block',
  props: {
    id: { type: Number, required: true },
    type: {
      type: String,
      required: true,
      validator: val => ['simple', 'normal'].includes(val),
    },
  },

  data() {
    return {
      highlighted: false,
      style: '_green',
    };
  },

  computed: {
    isStyleNormal() { return this.type === 'normal' ? this.style : ''; },
  },

  methods: {
    changeStyle() {
      if (this.type === 'normal') {
        if (this.style === '_red') {
          this.style = '_green';
        } else if (this.style === '_green') {
          this.style = '_red';
        }
      }
    },

    close() {
      if (this.type === 'normal') {
        // eslint-disable-next-line
        if (window.confirm('Are you sure?')) {
          this.$emit('close', { id: this.id, type: this.type, el: this.$el.classList });
        }
      } else {
        this.$emit('close', { id: this.id, type: this.type, el: this.$el.classList });
      }
    },

    highlight() {
      if (this.$el.classList.contains('_highlighted')) {
        this.highlighted = false;
        this.$emit('highlight', { status: 'false', el: this.$el.classList });
      } else {
        this.highlighted = true;
        this.$emit('highlight', { status: 'true', el: this.$el.classList });
      }
    },
  },
};
</script>

<style lang="scss" scoped>
  .block {
    height: 50px;
    width: 200px;
    position: relative;
    border: 1px solid #ccc;
    border-radius: 6px;
    margin: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    user-select: none;

    &__close {
      color: #777;
      cursor: pointer;
      font: 14px/100% arial, sans-serif;
      position: absolute;
      right: 5px;
      text-decoration: none;
      text-shadow: 0 1px 0 #fff;
      top: 5px;

      &:after {
        content: '✖';
      }
    }
  }
  ._green {
    border: 2px dotted green;
  }

  ._red {
    border: 2px dotted red;
  }

  ._highlighted {
    box-shadow: 0px 0px 12px 0px rgba(0,0,0,0.75);
  }
</style>
