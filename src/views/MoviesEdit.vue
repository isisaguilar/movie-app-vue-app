<template>
  <div class="movies-edit">
    <form v-on:submit.prevent="updateMovie()">
      <h1>Update Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="updateMovieParams.title" />
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="updateMovieParams.year" />
      </div>
      <input type="submit" value="Update" />
      <button v-on:click="destroyMovie()">Delete</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      updateMovieParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.updateMovieParams = response.data;
    });
  },

  methods: {
    updateMovie: function () {
      axios
        .patch(`/${this.updateMovieParams.id}`)
        .then((response) => {
          console.log(response.data);
          this.$router.push(`/${response.data.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    destroyMovie: function () {
      if (confirm("You sure about this?")) {
        axios.delete(`/${this.$route.params.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        });
      }
    },
  },
};
</script>
