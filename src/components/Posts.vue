<template>
  <div class="posts">
    <transition-group name="flip-list">
      <Post
        v-bind:key="post.id"
        v-for="post of posts.slice().reverse()"
        v-bind:post="post"
        v-on:gen-com="genCom"
        v-on:com-counter="countCom"
      >
      </Post>
    </transition-group>
  </div>
</template>


<script>
import Post from "@/components/Post";
import Comment from "./Comment";
export default {
  props: ["posts"],
  components: {
    Comment,
    Post,
  },
  mounted() {
    console.log(this.props);
  },
  methods: {
    countCom(id) {
      this.$emit("com-counter", id);
    },
    // genCom(id, count) {
    //   this.$emit("gen-com", id, count);
    // },
  },
};
</script>
<style>
.flip-list-move {
  transition: transform 1s;
}
</style>