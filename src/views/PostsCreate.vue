<template>
  <div class="New">
    <form v-on:submit.prevent="submit()">
      <h1>New Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <!-- <div>
        <label>User: </label>
        <input type="integer" v-model="newPostParams.user_id" />
      </div> -->
      <div>
        <label>Title: </label>
        <input type="text" v-model="newPostParams.title" />
      </div>
      <div>
        <label>Post: </label>
        <input type="text" v-model="newPostParams.body" />
      </div>
      <div>
        <label>image: </label>
        <input type="text" v-model="newPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newPostParams: {},
      errors: [],
    };
  },
  methods: {
    submit: function () {
      axios
        .post("/posts", this.newPostParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
