<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img
          src="https://th.bing.com/th/id/OIG.ZamPZFVt9awebaL9L2U0?w=1024&h=1024&rs=1&pid=ImgDetMain"
          alt="movies-banner"
          class="featured-img"
        />
        <div class="detail">
          <h3>Star-Movies</h3>
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Magni
            cupiditate eveniet quos error, vel voluptates nesciunt delectus modi
            omnis, molestiae suscipit? Perferendis dicta facere expedita! Eius
            quam inventore veniam explicabo!
          </p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="SearchMovies()" class="search-box">
      <input
        type="text"
        placeholder="What are you looking for ?"
        v-model="search"
      />

      <input type="submit" value="search" />
    </form>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie-Poster" />
            <div class="type">
              {{ movie.Type }}
            </div>
          </div>
          <div class="detail">
            <p class="y">
              {{ movie.Year }}
            </p>
            <h3>
              {{ movie.Title }}
            </h3>
          </div>
        </router-link>
        {{ movie.Title }}
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import env from "@/env.js";

export default {
  setup() {
    const movies = ref([]);
    const search = ref("");

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then((response) => response.json())
          .then((data) => {
            movies.value = data.Search;
            search.value = "";
            console.log(movies.value);
          });
      }
    };
    return {
      search,
      movies,
      SearchMovies,
    };
  },
};
</script>

<style lang="scss">
.home {
  margin-left: 40px;
  margin-right: 40px;
  .feature-card {
    position: relative;
    .featured-img {
      display: block;
      width: 100%;
      height: 500px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }
    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      padding: 16px;
      background-color: rgba(43, 64, 97, 0.6);

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
  }

  input {
    display: block;
    appearance: none;

    border: none;
    outline: none;
    background: none;

    &[type="text"] {
      width: 103%;
      color: white;
      background-color: rgb(95, 155, 252);
      font-size: 20px;
      padding: 10px 16px;
      border-radius: 8px;
      margin-bottom: 15px;
      transition: 0.4s;

      &::placeholder {
        color: white;
      }
      &:focus {
        color: rgb(255, 255, 255);
      }
    }
    &[type="submit"] {
      width: 103%;
      max-width: 300%;
      padding: 16px;
      border-radius: 8px;
      color: white;
      font-size: 20px;
      text-transform: uppercase;
      transition: 0.4s;

      &:active {
        color: rgb(86, 85, 85);
        background-color: beige;
      }
    }
  }

  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;

    .movie {
      max-width: 50%;
      flex: 1 1 50%;
      padding: 10px 8px;

      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;
      }
      .product-image {
        position: relative;
        display: block;

        img {
          display: block;
          width: 100%;
          height: 275px;
          object-fit: cover;
        }
        .type {
          position: absolute;
          padding: 8px 16px;
          background-color: antiquewhite;
          color: rgb(3, 40, 91);
          bottom: 16px;
          left: 0px;
          text-transform: capitalize;

        }
      }

      .detail{
        color: white;
        padding: 16px 8px;
        flex: 1 1 10%;
        border-radius: 8px;
        .y{
          color: white;
          font-size: 14px;

        }
        h3{
          color: antiquewhite;
          font-size: 18px;
        }
      }
    }
  }
}
</style>
