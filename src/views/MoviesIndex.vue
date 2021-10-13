<template>
  <div class="home">
    <h1>Movies</h1>
    <div>
      <button v-on:click="sortAttribute">Sort Alphabetically</button>
    </div>
    <!-- <div
      v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), 'title')"
      v-bind:key="movie.id"
    ></div> -->
    Search by name:
    <input v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">
        {{ movie.title }}
      </option>
    </datalist>
    <br />
    Search by title:
    <input v-model="titleFilter" />
    <div
      v-for="movie in orderBy(
        filterBy(movies, titleFilter, 'title'),
        sortAttribute
      )"
      v-bind:key="movie.id"
    >
      <div v-for="movie in movies" v-bind:key="movies.id">
        <h2>
          Movie: <br />
          {{ movie.title }}
          <router-link :to="`/movies/${movie.id}`">See Details</router-link>
        </h2>
      </div>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      movies: [],
      sortAttribute: "title",
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
