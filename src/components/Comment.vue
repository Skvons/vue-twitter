<template>
  <div class="comment">
    <div v-on:mouseover="popup" v-on:mouseout="popup" class="avatar">
      <div class="popup" v-if="this.showPopup">
        <span class="popuptext" id="myPopup">{{ comment.name }}</span>
      </div>
      <img v-bind:src="comment.photo" alt="" />
    </div>
    <div class="text">{{ comment.text }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showPopup: false,
    };
  },
  props: {
    postId: {
      type: Number,
      require: true,
    },
    comment: {
      type: Object,
      require: true,
    },
  },
  mounted() {
    this.$emit("com-counter", this.postId);
  },
  methods: {
    popup() {
      this.showPopup = !this.showPopup;
    },
  },
};
</script>
<style>
.popup {
  position: relative;
  cursor: pointer;
}

.popup .popuptext {
  width: 160px;
  background-color: #555;
  color: #fff;
  text-align: center;
  border-radius: 6px;
  padding: 8px 0;
  position: absolute;
  z-index: 1;
  bottom: 125%;
  left: 50%;
  margin-left: -80px;
}

.popup .popuptext::after {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: #555 transparent transparent transparent;
}
.comment {
  margin-bottom: 1rem;
  padding: 1rem;
  border-radius: 1rem;
  background-color: var(--background-color);
  display: flex;
  vertical-align: middle;
}

.avatar:hover + .popup {
  display: block;
}
</style>