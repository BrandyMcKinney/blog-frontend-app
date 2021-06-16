<template>
  <div class="posts-new">
    <img v-if="status" v-bind:src="`https://http.cat/${status}`" alt="" />

    <form v-on:submit.prevent="create()">
      <h1>New Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newPost.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="newPost.body" />
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="newPost.image" />
      </div>
      <input type="submit" value="Create" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newPost: {},
      errors: [],
      status: null,
    };
  },
  methods: {
    create: function () {
      var params = {
        title: this.newPost.title,
        body: this.newPost.body,
        image: this.newPost.image,
        user_id: this.newPost.user_id,
      };
      axios
        .post("/posts", params)
        .then((response) => {
          console.log("posts create", response.data);
          this.$router.push("/posts");
        })
        .catch((error) => {
          console.log("posts create error", error.response);
          this.errors = error.response.data.errors;
          this.status = error.response.status;
        });
    },
  },
};
</script>
