<template>
  <div class="home">
    <h1>Movies</h1>
    <img
      src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSlTgq6O8f0cGQMUZswl5FZdo0Q5ftt054mVQ&usqp=CAU"
      alt="movie meme"
      width="300"
      height="300"
    />
    <br />
    <div v-for="movie in movies" v-bind:key="movies.id">
      <div class="container">
        <h2>
          Movie: <br />
          {{ movie.title }}
        </h2>
        <div class="card text-center mx-auto" style="width: 18rem">
          <router-link :to="`/movies/${movie.id}`">
            <img
              src="https://i.ytimg.com/vi/h_LGCQ8Wwy0/maxresdefault.jpg"
              class="card-img-top"
              alt="spongebob at the movies"
            />
          </router-link>
          <div class="card-body">
            <h5 class="card-title">{{ movie.year }}</h5>
            <p class="card-text">
              {{ movie.plot }}
            </p>
          </div>
        </div>
      </div>
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
