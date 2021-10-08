<template>
  <div class="home">
    <h1>Movies</h1>
    <div v-for="movie in movies" v-bind:key="movies.id">
      <h2>
        Movie: <br />
        {{ movie.title }}
        <router-link :to="`/movies/${movie.id}`">See Details</router-link>
      </h2>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/one_movie").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
  },
};
</script>
