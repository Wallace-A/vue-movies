<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0083658">
        <img src="https://m.media-amazon.com/images/M/MV5BZmQ5NGFiNWEtMmMyMC00MDdiLTg4YjktOGY5Yzc2MDUxMTE1XkEyXkFqcGdeQXVyNTA4NzY1MzY@._V1_SX300.jpg" alt="Naruto Poster" class="featured-img" />
        <div class="detail">
          <h3>Blade Runner</h3>
          <p>Movie description</p>
        </div>
      </router-link>
    </div>
    <!-- @submit.prevent == prevent.default() -->
    <form @submit.prevent="SearchMovies()" class="search-box">
      <!-- v-model captures value of text and sets it as value search -->
      <input type="text" name="" id="" placeholder="What are you looking for?" v-model="search">
      <input type="submit" value="Search">
    </form>

    <div class="movies-list">
      <!-- v-for loops movie data -->
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Posyter">
            <div class="type">{{ movie.Type}} </div>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
//ref is similar to react hooks. 
import { ref} from "vue";
import env from "@/env.js";

export default {
  setup () {
    const search = ref("");
    const movies = ref ([]);
    const SearchMovies = () => {
      //check value of search from text input
      if(search.value != ""){
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
        .then(response => response.json())
        .then(data => {
          //store data
          movies.value = data.Search;
          //reset search input
          search.value = "";
        })
      }
    }
    return {
      search,
      movies,
      SearchMovies
    }
  }
  
}
</script>
<style lang="scss">
.home {
  .feature-card {
    position: relative;

    .featured-img {
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;

      position: relative;
      z-index: 0;
    }

    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;

      h3 {
        color: white;
        margin-bottom: 16px;
      }

      p {
        color: white;
      }
    }
  }

  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 16px;
    align-items: center;

    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;

      &[type="text"] {
        width: 100%;
        color: white;
        background-color: #496583;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 8px;
        margin-bottom: 15px;
        transition: 0.4s;

        &::placeholder {
          color: #F3F3F3;
        }

        &:focus {
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        }
      }

      &[type="submit"] {
        width: 100%;
        max-width: 300px;
        background-color: #42B883;
        padding: 16px;
        border-radius: 8px;
        color: white;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;

        &:active {
          background-color: #3B8070;
        }
      }
    }
  }
}
</style>