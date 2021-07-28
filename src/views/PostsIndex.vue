<template>
  <div class="home">
    <h2 v-for="post in posts">
      <p>{{ post.id }}</p>
      <router-link v-bind:to="`/posts/${post.id}`">
        <p>{{ post.title }}</p>
        <p>{{ post.image }}</p>
      </router-link>
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
      posts: [],
    };
  },
  created: function () {
    this.postIndex();
  },
  methods: {
    postIndex: function () {
      axios.get("/posts").then((response) => {
        console.log(response.data);
        this.posts = response.data;
      });
    },
  },
};
</script>
