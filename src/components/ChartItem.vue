<template>
  <div class="item">
    <div class="item__count">{{ post.comments }}</div>
    <div class="item__title">
      {{ post.text }}
    </div>
  </div>
</template>
<script>
export default {
  props: {
    post: {
      type: Object,
      require: true,
    },
  },
  methods: {
    getRandomInt(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min)) + min;
    },
  },
};
</script>
<style>
.top {
  padding: 0 1rem;
}
.item {
  margin: -1px -1px;
  padding: 1rem;
  border-bottom: 0.1rem black solid;
  border-color: var(--border-color);
  justify-content: flex-start;
  display: flex;
  flex-direction: row;
}

.item__count {
  color: var(--background-color);
  height: 2rem;
  width: 2rem;
  border-radius: 1rem;
  padding: 0.5rem;
  background-color: var(--button-color);
}

.item__title {
  text-align: center;
  padding: 0.5rem;
}
</style>