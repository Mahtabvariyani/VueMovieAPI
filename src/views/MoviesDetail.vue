<template>
  <div class="movie-detail">
    <h2>{{ movie.Title }}</h2>

    <h3>
      {{ movie.Director }}
    </h3>
    <p>
      {{ movie.Country }}
    </p>
    <p>
      {{ movie.DVD }}
    </p>
    <p>
      {{ movie.Rated }}
    </p>
    <p>
      {{ movie.Writer }}
    </p>
    <p>
      {{ movie.Runtime }}
    </p>
    <p>
      {{ movie.Writer }}
    </p>
    <p>
      {{ movie.Language }}
    </p>
    <p>
      {{ movie.Released }}
    </p>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from "@/env.js";

export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(
        `http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`
      )
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
          movie.value = data;
        });
    });

    return {
      movie,
    };
  },
};
</script>

<style>
.movie-detail {
  color: white;
}
</style>
