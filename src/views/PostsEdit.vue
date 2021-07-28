<template>
  <div class="Edit">
    <form v-on:submit.prevent="submit()">
      <h1>Edit Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <!-- <div>
        <label>User: </label>
        <input type="integer" v-model="editPostParams.user_id" />
      </div> -->
      <div>
        <label>Title: </label>
        <input type="text" v-model="editPostParams.title" />
      </div>
      <div>
        <label>Post: </label>
        <input type="text" v-model="editPostParams.body" />
      </div>
      <div>
        <label>image: </label>
        <input type="text" v-model="editPostParams.image" />
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
      editPostParams: {},
      errors: [],
    };
  },
  created: function () {
    this.getPost();
  },
  methods: {
    submit: function () {
      axios
        .patch(`/posts/${this.$route.params.id}`, this.editPostParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/posts/" + this.$route.params.id);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    getPost: function () {
      axios.get(`/posts/${this.$route.params.id}`).then((response) => {
        this.editPostParams = response.data;
      });
    },
  },
};
</script>
