<template>
  <div class="show">
    <h2>
      <p>{{ post.id }}</p>
      <p>{{ post.title }}</p>
      <p>{{ post.body }}</p>
      <p>{{ post.image }}</p>
      <hr>
    </h2>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    this.postShow();
  },
  methods: {
    postShow: function () {
      axios.get(`/posts/${this.$route.params.id}`).then((response) => {
        console.log(response.data);
        this.post = response.data;
      });
    },
  },
};
</script>
