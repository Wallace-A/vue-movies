<template>
  <div class="movie-detail">
      <h2>MOVIE TITLE</h2>
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
                console.log(data);
            })
        });

        return{
            movie
        }
    }
}
</script>

<style>

</style>