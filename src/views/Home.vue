<template>
  <div class="home">
    <h1>Movies</h1>
    <img
      src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSlTgq6O8f0cGQMUZswl5FZdo0Q5ftt054mVQ&usqp=CAU"
      alt="movie meme"
      width="300"
      height="300"
    />
    <div v-for="movie in movies" v-bind:key="movies.id">
      <h2 style="border: 2px solid Tomato">
        Movie: {{ movie.title }} {{ movie.year }}
      </h2>
    </div>
    <div style="border: 5px solid DodgerBlue">
      Title:
      <input type="text" v-model="newMovie.title" />
    </div>
    <div style="border: 5px solid DodgerBlue">
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
