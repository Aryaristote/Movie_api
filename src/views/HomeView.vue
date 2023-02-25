<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt1905041">
        <img src="https://m.media-amazon.com/images/M/MV5BMTM3NTg2NDQzOF5BMl5BanBnXkFtZTcwNjc2NzQzOQ@@._V1_SX300.jpg" 
        alt="Top Gun" class="feature-img">
        <div class="details">
            <h1 block-title>MOST <br>WATCHED</h1>
          <h3>"Fast & Furious 6"</h3>
          <p>Since Dom (Diesel) and Brian's (Walker) Rio heist toppled a kingpin's empire and left their crew <br>with $100 million, our 
            heroes have scattered across the globe. But their inability to ....</p>
          <small><b>Year: </b>2013</small><br>
          <small><b>With:</b> Vin Diesel, Paul Walker, Dwayne Johnson</small>
        </div>
      </router-link>
    </div>
    <div class="search-block">
      <form @submit.prevent="searchMovies()" class="search-box">
        <input type="text" placeholder="Type the movie title" v-model="search">
        <input type="submit" value="Search">
      </form>
      <div class="fav-btn">
        <button>My Favorite ({{ favMovies.length }})</button>
      </div>
    </div>

    <div class="movie-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster">
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="details">
            <h3>{{ movie.Title }}</h3>
            <p class="year">{{ movie.Year }}</p>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import env from '@/env.js';
import favMovies from '../storage/favMovie';

export default {
  name: 'HomeView',
  data() {
    return {
      favMovies,
    }
  },
  setup() {
    const search = ref("");
    const movies = ref([]);

    const searchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then(response => response.json())
          .then(data => {
            movies.value = data.Search;
            search.value = "";
          })
      }
    }

    return { search, movies, searchMovies }
  }
}
</script>

<style lang="scss">
  .home {

    .feature-card{
      position: relative;
      height: 300px;
      width: 100%;

      .feature-img{
        height:100%;
        width: 100%;
        object-fit:cover;
      }

      .details{
        height: 100%;
        position: absolute;
        left: 0;
        right: 0;
        bottom: 0;
        background-color: rgba(0, 0, 0, .6);
        padding: 16px;
        z-index: 1;

        h1{
          color: white;
          font-size: 70px;
        }

        h3{
          color: white;
          margin-bottom: 10px;
          font-size: 25px;;
        }

        p{
          color: white;
        }
      }
    }

    .search-block{
      width: 100%;
      display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;

      .search-box{
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        padding: 25px 16px 16px 0;
        width: 50%;

        input{
          display: block;
          appearance: none;
          border: none;
          outline: none;
          background: none;

          &[type="text"] {
            width: 65%;
            color: fff;
            background-color: transparent;
            font-size: 18px;
            padding: 11px 20px;
            margin-bottom: 15px;
            transition: .4s;
            border: 4px solid #75c8a3;
            border-right: none;
            border-radius: 35px 0 0 35px;

            @media (max-width: 867px) {
              font-size: 12px;
              padding: 9px 20px;
            }

            &::placeholder{
              color: #f3f3f3;
            }

            &::focus{
              box-shadow: 0px 3px 6px rgba(0, 0, 0, .2);
              border: 2px solid #42B883;
            }
          }

          &[type="submit"]{
            width: 35%;
            background-color: #42B883;
            padding: 13px;
            color: #fff;
            font-size: 20px;
            margin: -15px 0 0 -10px;
            text-transform: uppercase;
            transition: 0.4s;
            border-radius: 0 35px 35px 0;

            @media (max-width: 867px) {
              font-size: 12px;
            }

            &:hover{
              background-color: #3b8080;
            }
          }
        }
      }

      .fav-btn{
        
        button{
          border: 4px solid #42B883;
          background-color: transparent;
          padding: 13px 35px;
          font-size: 17px;
          border-radius: 35px;
          color: #42B883;
          font-size: bold;

          @media (max-width: 867px) {
            font-size: 12px;
            padding: 9px 20px;
          }

          &:hover{
            background-color: #42B883;
            color: white;
          }
        }
      }
    }
    
    .movie-list{
      display: flex;
      flex-wrap: wrap;
      margin: 0 8px;

      .movie{
        max-width: 50%;
        flex: 1fr 1fr 1fr 1fr;
        width: 25%;
        padding: 16px 8px;

        @media (max-width: 867px) {
          max-width: 50%;
          flex: 1fr 1fr 1fr 1fr;
          width: 50%;
          padding: 16px 8px;
        }

        .movie-link{
          display: flex;
          flex-direction: column;
          height: 100%;

          .product-image{
            position: relative;
            display: block;
            
            img{
              display: block;
              width: 100%;
              height: 275px;
              object-fit: cover;
            }

            .type{
              position: absolute;
              padding: 8px 16px;
              background-color: #42B883;
              color: white;
              bottom: 16px;
              left: 0;
              text-transform: capitalize;
            }
          }

          .details{
            background-color: #496583;
            padding: 16px 8px;
            flex: 1 1 100%;
            border-radius: 0px 0px 8px 8px;

            .year{
              color: #aaa;
              font-size: 14px;
            }

            h3{
              color: white;
              font-weight: 600;
              font-size: 18px;
            }
          }
        }
      }
    }
  }
</style>
