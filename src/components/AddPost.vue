<template>
  <form @submit.prevent="onSubmit" class="form">
    <input
      id="formInput"
      required
      class="form__input"
      type="text"
      placeholder="О чём вы думаете?"
      v-model="text"
    />
    <button type="submit">Поделиться</button>
  </form>
</template>
<script>
var newDate = new Date(Date.now());
export default {
  data() {
    return {
      text: "",
    };
  },

  methods: {
    getImg() {
      return this.text.match(/http[^ ]+/g)
        ? this.text.match(/http[^ ]+/g)
        : null;
    },

    setId() {
      return JSON.parse(localStorage.getItem("posts"))
        ? JSON.parse(localStorage.getItem("posts")).length
        : 0;
    },

    getText() {
      return this.text.replace(this.text.match(/http[^ ]+/g), "");
    },

    onSubmit() {
      if (this.text.trim()) {
        const newPost = {
          comments: 0,
          photo: this.getImg(),
          id: this.setId(),
          text: this.getText(),
          date: newDate.toDateString("ru"),
        };
        this.$emit("add-post", newPost);
      }
      document.querySelector("#formInput").value = "";
    },
  },
};
</script>
<style >
.form {
  border: 0.1rem black solid;
  border-color: var(--border-color);
  padding: 2rem;
  margin-bottom: -0.1rem;
  display: flex;
  justify-content: space-between;
}

.form__input {
  padding: 0.5rem 1rem;
  border-radius: 1rem;
  border: 0.1rem black solid;
  border-color: var(--border-color);
  width: 100%;
  margin-right: 1rem;
}
</style>