<template>
  <div class="movie-detail">
      <img :src="movie.Poster" alt="Movie Poster" class="featured-img">
      <h2>{{ movie.Title }}</h2>
      <p> {{ movie.Year }}</p>
      <p>{{ movie.Plot}}</p>
  </div>
</template>

<script>
import {ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from "@/env.js";

export default {
    setup () {
        const movie = ref({});
        //can't use $route to get id, need to use useRoute instead
        const route = useRoute();

        onBeforeMount(() => {
            fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
            .then(response => response.json())
            .then(data => {
                movie.value = data;
            })
        });

        return{
            movie
        }
    }
}
</script>

<style lang="scss">

.movie-detail {
    padding: 16px;

    h2{
        color: white;
        font-size: 28px;
        font-weight: 600;
        margin-bottom: 16px;
    }
    
    .featured-img{
        display: block;
        max-width: 200px;
        margin-bottom: 16px;
    }

    p {
        color: white;
        font-size: 18px;
        line-height: 1.4;
    }


}
</style>