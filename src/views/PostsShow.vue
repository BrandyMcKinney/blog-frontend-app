<template>
  <div class="Posts-Show">
    <h1>All Posts</h1>
    <div v-for="post in posts" v-bind:key="post.id">
      <h2>Title:</h2>
      <p>{{ post.title }}</p>
      <h2>Body:</h2>
      <p>{{ post.body }}</p>
      <h2>Image:</h2>
      <p>{{ post.image }}</p>
      <h2>User:</h2>
      <p>{{ post.user_id }}</p>
      <router-link to="/posts">Back to All Posts</router-link>
      <button v-if="recipe.is_owner" v-on:click="destroyRecipe()">Destroy recipe</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get("/posts/" + this.$route.params.id).then((response) => {
      console.log("posts show", response);
      this.post = response.data;
    });
  },
  methods: {},
};
</script>
