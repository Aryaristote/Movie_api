<template>
  <div class="container movie-detail">
    <div class="left-block">
      <img :src="movie.Poster" alt="image plot">
    </div>
    <div class="right-block">
      <h1>{{ movie.Title }}</h1>
      <p class="plot">{{ movie.Plot }}</p>
      <p class="year"><b>Year:</b> {{ movie.Year }}</p>
      <p class="runtime"><b>Durtaion:</b> {{ movie.Runtime }}</p>
      <p class="gender"><b>Gender:</b> {{ movie.Genre }}</p>
      <p class="director"><b>Director:</b> {{ movie.Director }}</p>
      <p class="actors"><b>Actors:</b> {{ movie.Actors }}</p>
      <div class="fav-btn">
        <button @click="addFavorite">Make Favorite {{ favMovie }}</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';
import favMovie from '../storage/favMovie';

export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
        .then(response => response.json())
        .then(data => {
          console.log(data)
          movie.value = data;
        })
    });

    const addFavorite = () => {
      if (favMovie.every(fav => fav.imdbID !== movie.value.imdbID)) {
        favMovie.push(movie.value)
      }
      console.log(favMovie);
        // favMovie.push(movie.value)
    }

    return {
      movie, addFavorite, 
    }
  },
}
</script>

<style lang="scss">
  .container {
    width: 80%;
    margin-top: 20px;
  }

  .container {
    @media (min-width: 250px) {
      width: 90%;
    }
    @media (min-width: 576px) {
      width: 90%;
    }
  }
  .movie-detail{
    padding: 16px 8px;
    display: flex;
    flex-direction: row;
    gap: 25px;
    justify-content: center;
    align-items: center;
    color: #b2b4b5;

    .right-block{
      
      h1{
        font-size: 34px;
        padding: 8px 0;
      }

      .plot{
        margin: 15px 0;
      }

      .fav-btn{
        margin: 20px 0 0 0;

        button{
          border: none;
          background-color: #42B883;
          padding: 12px 30px;
          font-size: 17px;
          border-radius: 35px;
          color: #fff;
          font-size: bold;

          @media (max-width: 867px) {
            font-size: 12px;
            padding: 9px 20px;
          }

          &:hover{
            opacity: .8;
            cursor: pointer;
          }
        }
      }
    }
  }
</style>