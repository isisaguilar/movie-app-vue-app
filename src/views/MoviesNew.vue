<template>
  <div class="movies-new" style="color: white">
    <form v-on:submit.prevent="createMovie()">
      <h1>Create New Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newMovieParams.title" />
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="newMovieParams.year" />
      </div>
      <div>
        <label>Plot:</label>
        <input type="text" v-model="newMovieParams.plot" />
        <br />
        <small> {{ 50 - newMovieParams.plot.length }}charecters left </small>
      </div>
      <input type="submit" value="Create" />
    </form>
    <img
      src="https://c.tenor.com/gQf-Nf3he8cAAAAd/cat-typing.gif"
      alt="cat typing meme"
      width="300"
      height="300"
    />
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newMovieParams: {
        plot: "",
      },
      errors: [],
      plot: "",
    };
  },
  methods: {
    createMovie: function () {
      axios
        .post("http://localhost:3000/one_movie", this.newMovieParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
