<template>
  <div id="app">
    <div id="nav">
      <li><router-link to="/">Home</router-link></li>
      <li><router-link to="/about">About</router-link></li>
      <li><router-link to="/sample">Sample</router-link></li>
      <li><router-link to="/sample2">Sample2</router-link></li>
      <li class="nav-item" v-if="!isLoggedIn()">
        <router-link class="nav-item" to="/signup">Signup</router-link>
      </li>
      <li class="nav-item" v-if="!isLoggedIn()">
        <router-link class="nav-link" to="/login">Login</router-link>
      </li>
      <li class="nav-item" v-if="isLoggedIn()">
        <router-link class="nav-link" to="/logout">Logout</router-link>
      </li>
      <li><router-link to="/posts">All Posts</router-link></li>
      <li><router-link to="/posts/new">New Post</router-link></li>
    </div>

    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <a class="navbar-brand" href="#">Le Blog</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <a class="nav-link" href="#">
              Home
              <span class="sr-only">(current)</span>
            </a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Link</a>
          </li>
          <li class="nav-item dropdown">
            <a
              class="nav-link dropdown-toggle"
              href="#"
              id="navbarDropdown"
              role="button"
              data-toggle="dropdown"
              aria-haspopup="true"
              aria-expanded="false"
            >
              Dropdown
            </a>
            <div class="dropdown-menu" aria-labelledby="navbarDropdown">
              <a class="dropdown-item" href="#">Action</a>
              <a class="dropdown-item" href="#">Another action</a>
              <div class="dropdown-divider"></div>
              <a class="dropdown-item" href="#">Something else here</a>
            </div>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
          </li>
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search" />
          <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
        </form>
      </div>
    </nav>
    <div class="container">
      <div v-if="flashMessage" v-on:click="flashMessage = null" class="alert alert-success" role="alert">
        {{ flashMessage }}
      </div>
      <router-view />
    </div>
  </div>
</template>

<style>
body {
  background-image: url("./assets/spring.png");
}
#app {
  font-family: monaco, Consolas, Lucida Console, monospace;
}
.navbar-brand {
  font-family: "Monaco", cursive;
  font-size: 5em;
}
</style>
<script>
export default {
  data: function () {
    return {
      flashMessage: null,
    };
  },
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
  },
};
</script>
