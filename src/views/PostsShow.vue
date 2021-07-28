<template>
  <div class="show">
    <h2>
      <p>{{ post.id }}</p>
      <p>{{ post.title }}</p>
      <p>{{ post.body }}</p>
      <p>{{ post.image }}</p>
      <hr>
    </h2>
    <router-link v-bind:to="`/posts/${post.id}/edit`">Edit</router-link>
    <br/>
    <br/>
    <button v-on:click="postDelete()">Delete</button>
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
    postDelete: function () {
      axios.delete(`/posts/${this.$route.params.id}`).then((response) => {
        console.log(response.data);
        this.$router.push("/posts/");
      });
    },
  },
};
</script>
