<template>
  <div class="movies-show">
    <h2>Title: {{ currentMovie.title }}</h2>
    <p>Year: {{ currentMovie.year }}</p>
    <p>Plot: {{ currentMovie.plot }}</p>
    <router-link
      type="button"
      class="btn btn-info"
      :to="`/movies/${currentMovie.id}/edit`"
      >Edit Movie</router-link
    >
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      currentMovie: {},
    };
  },
  created: function () {
    axios.get(`/one_movie/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.currentMovie = response.data;
    });
  },
  methods: {},
};
</script>
