<template>
  <div class="Posts-Index">
    <h1>All Posts</h1>
    <div>
      Search by title:
      <input type="text" v-model="searchFilter" />
    </div>
    <div
      class="row"
      is="transition-group"
      enter-active-class="animated rotateIn"
      leave-active-class="animated rotateOut"
    >
      <div class="col-sm-7" v-for="post in filterBy(posts, searchFilter, 'title')" v-bind:key="post.id">
        <div class="card">
          <h5 class="card-title">{{ post.title }}</h5>
          <div class="card-body">
            <img v-bind:src="post.image" class="card-img-url" alt="..." />

            <p class="card-text">{{ post.body }}</p>
            <a href="#" class="btn btn-primary">More Info</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.card img {
  object-fit: cover;
  height: 200px;
}
</style>
<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      posts: [],
      searchFilter: "",
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("/posts").then((response) => {
        console.log("posts index", response);
        this.posts = response.data;
      });
    },
  },
};
</script>
