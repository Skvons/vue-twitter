<template>
  <div class="chart">
    <h1 class="chart__title">Поулярные темы</h1>
    <div class="top">
      <ChartItem
        v-bind:key="post.id"
        v-for="post of posts"
        v-bind:post="post"
      />
    </div>
    <div class="empty" v-if="posts.length < 1">
      <h2>Тем нет</h2>
    </div>
    <slot> </slot>
  </div>
</template>

<script>
import ChartItem from "@/components/ChartItem";
export default {
  props: ["posts"],
  components: {
    ChartItem,
  },
};
</script>
<style>
.chart__title {
  margin: 0 -0.1rem;
  padding: 1rem;
  border: 0.1rem black solid;
  border-color: var(--border-color);
}
.chart {
  border-radius: 1rem;
  color: var(--font-color);
}
</style>