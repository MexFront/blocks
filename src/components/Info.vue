<template lang="pug">
  .info
    .info__total Всего блоков на странице: {{ total }}
    .info__highlited Всего выделенных блоков: {{ highlighted }}
    .info__green Количество выделенных зеленых: {{ green }}
    .info__red Количество выделенных красных: {{ red}}
</template>

<script>
export default {
  name: 'Info',
  props: {
    green: { type: Number, default: 0 },
    highlighted: { type: Number, default: 0 },
    red: { type: Number, default: 0 },
    total: { type: Number, default: 0 },
  },
};
</script>
