<template>
  <div class="home">
    <h1>Movies</h1>
    <div v-for="movie in movies" v-bind:key="movies.id">
      <h2>Movie: {{ movie.title }} {{ movie.year }}</h2>
    </div>
    <div>
      Title:
      <input type="text" v-model="newMovie.title" />
    </div>
    <div>
      Year:
      <input type="text" v-model="newMovie.year" />
    </div>
    <button v-on:click="createMovie()">Create Movie</button>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
      newMovie: {},
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
    createMovie: function () {
      var params = {
        title: "Onward",
        year: 2020,
      };
      axios.post("http://localhost:3000/one_movie", params).then((response) => {
        console.log(response.data);
        this.movies.push = response.data;
      });
    },
  },
};
</script>
