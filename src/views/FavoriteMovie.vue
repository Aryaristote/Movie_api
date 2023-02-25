<template>
    <h1>Favorite Movies</h1><br>
    <div class="movie-list" v-if="favMovies.length">
        <div class="movie" v-for="(favMovie, index) in favMovies" :key="index">
            <div class="product-image">
                <img :src="favMovie.Poster" alt="Movie Poster">
            </div>
            <div class="details">
                <h3>{{ favMovie.Title }}</h3>
                <p class="year">favMovie.Year</p>
            </div>
            <div class="fav-btn">
                <button @click="removeFav(index)">Remove Favourite</button>
            </div>
        </div>
    </div>
    <div v-else>
        <p>No favourite movie added... </p>
    </div>
    
</template>

<script>
import favMovies from '../storage/favMovie';

export default {
    data() {
        favMovies,
            console.log(favMovies);
        return {
            favMovies,
        }
    },

    methods: {
        removeFav(index) {
            this.favMovies.splice(index, 1);
        }
    }
}
</script>

<style lang="scss">
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
</style>