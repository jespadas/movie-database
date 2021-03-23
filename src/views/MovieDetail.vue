<template>
  <div class="movie-detail">
    <h2>{{ movie.Title }}</h2>
    <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
    <p>{{ movie.Plot }}</p>
    <p>More details :</p>
    <span>Year : {{ movie.Year }}</span>
    <span>Cast : {{ movie.Actors }}</span>
    <span>Director : {{ movie.Director }}</span>
  </div>
</template>
<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from "../env";

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
          movie.value = data;
        });
    });

    return {
      movie,
      route,
    };
  },
};
</script>
<style lang="scss">
.movie-detail {
  padding: 16px;
  display: flex;
  flex-direction: column;
  align-items: center;

  h2 {
    color: #fff;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
  }

  .featured-img {
    max-width: 200px;
    margin-bottom: 16px;
  }

  p {
    color: #fff;
    font-size: 18px;
    line-height: 1.4;
    text-align: justify;
  }

  span {
    color: #fff;
    font-size: 18px;
    line-height: 1.4;
    text-align: left;
  }
}
</style>
