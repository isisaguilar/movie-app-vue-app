<template>
  <div class="movies-show">
    <h2>{{ movie.title }}</h2>
    <p>{{ movie.year }}</p>
    <p>{{ movie.plot }}</p>
    <router-link :to="`/${movie.id}/edit`"> Edit </router-link>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios.get(`/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {},
};
</script>
