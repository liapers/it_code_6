<template>
  <div id="app">
    <HeaderKino />
    <div class="container">
      <div class="menuFilms">
        <SearchKino @search-kino="SaveSearch" />
        <ReitingFilms @sort-films="SortByReiring" />
      </div>
      <ul class="card-film flex">
        <CardFilm
          v-for="films in films"
          :key="films.kinopoiskId"
          :films="films"
        />
      </ul>
    </div>
  </div>
</template>

<script>
import HeaderKino from "./components/HeaderKino.vue";
import SearchKino from "./components/SearchKino.vue";
import CardFilm from "./components/CardFilm.vue";
import ReitingFilms from "./components/ReitingFilms.vue";
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      films: [],
      search: "",
      sort: false,
    };
  },
  components: {
    HeaderKino,
    SearchKino,
    CardFilm,
    ReitingFilms,
  },
  computed: {
    //фильтруем фильмы
    FilterFilm() {
      return this.films;
    },
  },
  beforeMount() {
    this.GetFilms();
  },
  methods: {
    //Получить фильмы
    GetFilms() {
      axios(
        `https://kinopoiskapiunofficial.tech/api/v2.2/films?${
          this.sort ? `order=RATING&type=ALL` : `order=YEAR&type=ALL`
        }&ratingFrom=0&ratingTo=10&yearFrom=1000&yearTo=3000&page=1${
          this.search != "" ? `&keyword=${this.search}` : ""
        }`,
        {
          method: "GET",
          headers: {
            "X-API-KEY": process.env.VUE_APP_KEY,
            "Content-Type": "application/json",
          },
        }
      )
        .then((json) => this.SaveFilms(json.data))
        .catch((err) => console.log(err));
    },
    //сохраняем фильмы
    SaveFilms(data) {
      this.films = data.items;
    },
    //ищем фильмы по ключевым словам
    SaveSearch(data) {
      this.search = data.search;
      this.GetFilms();
    },
    //сортируем фильмы
    SortByReiring(data){
      this.sort = data.flagSort;
      this.GetFilms();
    }
  },
};
</script>

<style>
*,
*::after,
*::before {
  box-sizing: inherit;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 16px;
}

.flex {
  display: flex;
  flex-wrap: wrap;
}

ul {
  margin-left: 0; /* Отступ слева в браузере IE и Opera */
  padding-left: 0; /* Отступ слева в браузере Firefox, Safari, Chrome */
  padding-top: 20px;
  margin-bottom: 0;
}

li {
  list-style-type: none;
}

img {
  max-width: 100%;
}

.container {
  margin: 0 auto;
  width: 1170px;
}

.card-film {
  justify-content: center;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
