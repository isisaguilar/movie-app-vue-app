<template>
  <div id="app" style="background-color: rgb(181, 73, 54)">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/movies">Movies</router-link> |
      <router-link to="/movies/new">Movies New</router-link> |
      <span v-if="!isLoggedIn()">
        <router-link to="/signup">Signup</router-link> |
      </span>
      <span v-if="!isLoggedIn()">
        <router-link to="/login">Login</router-link> |
      </span>

      <router-link to="/logout">Logout</router-link>
    </div>
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>

<script>
export default {
  data: function () {
    return {
      flashMessage: "",
    };
  },
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
    getId: function () {
      return localStorage.user_id;
    },
  },
};
</script>
