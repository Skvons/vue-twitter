<template>
  <div id="app" v-bind:class="{ darkTheme: darkTheme }">
    <div class="main">
      <div class="feed">
        <AddPost @add-post="addPost" />
        <Posts
          v-bind:posts="posts"
          @com-counter="comCounter"
          @gen-com="genCom"
        />
        <div class="empty" v-if="posts.length < 1">
          <h1>Постов пока нет</h1>
        </div>
        <button
          v-if="posts.length > 0"
          class="clearButton"
          v-on:click="this.storageClear"
        >
          Очистить
        </button>
      </div>
      <div class="chart-wrapper">
        <Chart v-bind:posts="posts">
          <button class="change-button" v-on:click="this.swithTheme">
            Изменить тему
          </button>
        </Chart>
      </div>
    </div>
  </div>
</template>

<script>
import Posts from "@/components/Posts";
import AddPost from "@/components/AddPost";
import Chart from "@/components/Chart";

export default {
  name: "App",
  data() {
    return {
      darkTheme: true,
      posts: [],
    };
  },

  mounted() {
    localStorage.getItem("posts") === null
      ? localStorage.setItem("posts", JSON.stringify(this.posts))
      : (this.posts = JSON.parse(localStorage.getItem("posts")));
  },

  methods: {
    swithTheme() {
      this.darkTheme = !this.darkTheme;
    },
    comCounter(id) {
      this.posts[id].comments++;
    },
    storageClear() {
      localStorage.clear();
      this.posts = [];
    },
    addPost(post) {
      this.posts.push(post);
      localStorage.setItem("posts", JSON.stringify(this.posts));
    },
  },
  components: {
    Posts,
    AddPost,
    Chart,
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
.change-button {
  margin: 1rem;
}
button {
  padding: 0.5rem 1rem;
  border-radius: 1rem;
  background-color: var(--button-color);
  color: var(--background-color);
  border: none;
  transition: 0.2s;
}

button:hover {
  background-color: var(--hover-color);
}

.clearButton {
  margin: 1rem;
}

.empty {
  color: var(--font-color);
}
.main {
  padding-top: 5rem;
  min-height: 100vh;
  display: grid;
  grid-template-columns: 2fr 1fr;
  margin: 0 auto;
  background-color: var(--background-color);
  max-width: 70rem;
}
.chart-wrapper {
  margin-left: 1px;
  max-height: 30vh;
  min-height: 10rem;
  flex-grow: 1;
}
.feed {
  margin-right: -1px;
  flex-grow: 1;
}
.darkTheme {
  background-color: #222831 !important;
  --button-color: #f2a365 !important;
  --border-color: #ececec !important;
  --font-color: #ececec !important;
  --background-color: #222831 !important;
  --hover-color: #f3c19b !important;
}
body {
  margin: 0;
  background-color: var(--background-color);
}
html {
  background-color: white;
  font-size: 16px;
  --hover-color: rgb(140, 140, 195);
  --button-color: rgb(83, 83, 195);
  --border-color: rgb(187, 187, 187);
  --font-color: #131313;
  --background-color: white;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
