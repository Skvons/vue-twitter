<template>
  <div class="post">
    <div class="user">
      <div class="avatar">
        <img
          src="https://images.unsplash.com/photo-1438761681033-6461ffad8d80?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80"
          alt=""
        />
      </div>
      <div class="name">
        <span><b>You</b></span>
        <span class="date">at {{ post.date }}</span>
      </div>
    </div>

    <div class="text">
      <div class="post-img">
        <img v-if="post.photo" v-bind:src="post.photo" alt="" />
      </div>
      <p class="title">{{ post.text }}</p>
    </div>
    <span class="comment__title" v-if="this.post.comments > 0">Коментарии</span>
    <div class="comments" style="text-align: left">
      <Comment
        v-on:com-counter="countCom"
        v-bind:postId="post.id"
        v-bind:key="comment.id"
        v-bind:comment="comment"
        v-for="comment in this.comments"
      />
    </div>
  </div>
</template>
<script>
import Comment from "./Comment";
export default {
  data() {
    return {
      users: [
        {
          name: "John Doe",
          photo:
            "https://images.unsplash.com/photo-1501196354995-cbb51c65aaea?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1351&q=80",
        },
        {
          name: "Alexa Clark",
          photo:
            "https://images.unsplash.com/photo-1488426862026-3ee34a7d66df?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=634&q=80",
        },
        {
          name: "Guccu Dima",
          photo:
            "https://images.unsplash.com/photo-1497551060073-4c5ab6435f12?ixlib=rb-1.2.1&ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&auto=format&fit=crop&w=667&q=80",
        },
      ],
      lorem: [
        "ipsum",
        "dolor",
        "sit",
        "amet",
        "consectetur",
        "adipiscing",
        "elit",
        "sed",
        "do",
        "eiusmod",
        "tempor",
        "incididunt",
        "ut",
        "labore",
        "et",
        "dolore",
        "magna",
        "aliqua",
        "enim",
        "ad",
        "minim",
        "veniam",
        "quis",
        "nostrud",
        "exercitation",
        "ullamco",
        "laboris",
        "nisi",
        "aliquip",
        "ex",
        "em",
      ],
      comments: [],
    };
  },
  props: {
    post: {
      type: Object,
      require: true,
    },
  },
  components: {
    Comment,
  },
  mounted() {
    for (let i = 0; i < 3; i++) {
      this.getCom();
      this.$forceUpdate;
      this.$emit("gen-com", this.post.id, this.comments.length);
    }
  },
  methods: {
    countCom(id) {
      this.$emit("com-counter", id);
    },

    loremIpsum() {
      let ipsum = "";
      for (let i = 0; i < this.getRandomInt(10, 50); i++) {
        ipsum = ipsum + `${this.lorem[this.getRandomInt(0, 31)]} `;
      }
      ipsum = ipsum[0].toUpperCase() + ipsum.slice(1);
      return ipsum;
    },

    getRandomInt(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min)) + min;
    },

    getCom() {
      setTimeout((user = this.getRandomInt(0, this.users.length)) => {
        this.comments.push({
          id: this.getRandomInt(10, 50),
          name: this.users[user].name,
          photo: this.users[user].photo,
          text: this.loremIpsum(),
        });
      }, this.getRandomInt(1000, 3000));
    },
  },
};
</script>




<style >
.comments {
  padding-top: 1rem;
  border-top: 0.1rem black solid;
  border-color: var(--border-color);
}
.date {
  font-size: 0.8rem;
  color: var(--font-color);
}
.user {
  display: flex;
  margin-bottom: 1rem;
}

.name {
  color: var(--font-color);
  text-align: left;
  display: flex;
  flex-direction: column;
}

.name span {
  margin-bottom: 0.5rem;
}

.post {
  color: var(--font-color);
  background-color: var(--background-color);
  display: flex;
  flex-direction: column;
  padding: 2rem;
  border: 0.1rem black solid;
  border-color: var(--border-color);

  margin-bottom: -0.1rem;
}
.comment__title {
  text-align: left;
  margin-bottom: 1rem;
}
.title {
  margin-bottom: 3rem;
  color: var(--font-color);
  font-size: 1.5rem;
  text-align: left;
}

.post-img img {
  object-fit: cover;
  max-height: 30rem;
  width: 100%;
  margin-right: 0 !important;
  border-radius: 1rem !important;
}

.avatar {
  border-radius: 50%;
  margin-right: 1rem;
}
.avatar img {
  border-radius: 50%;
  object-fit: cover;
  width: 50px;
  height: 50px;
}
</style>