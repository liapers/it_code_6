<template>
  <div  class="infoFilm flex">
    <div class="posterFilmInModal">
      <img :src="poster" :alt="film.nameRu" />
    </div>
    <div class="infoAboutFilm">
      <h2 v-if="film.nameRu" class="infoAboutFilm-name">{{ film.nameRu }}</h2>
      <h2 v-if="film.nameEn" class="infoAboutFilm-nameEn">
        {{ film.nameEn }}
      </h2>
      <h2 class="infoAboutFilm-nameOR">{{ film.nameOriginal }}</h2>
      <p class="infoAboutFilm-detail"><b>Год выпуска:</b> {{ film.year }}</p>
      <p class="infoAboutFilm-detail">
        <b>Страна:</b> {{ film.countries[0].country }}
      </p>
      <p class="infoAboutFilm-detail">
        <b>Жанр:</b> {{ film.genres[0].genre }}
      </p>
      <p class="infoAboutFilm-detail">
        <b>Рейтинг:</b> {{ film.ratingKinopoisk }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "ModalWindow",
  props: {
    film: { type: Object },
    errorReiting: { type: String },
    poster: {type: String}
  },
};
</script>

<style>
.infoFilm {
  padding: 5px;
  flex-direction: row;
  flex-wrap: nowrap;
}
.posterFilmInModal {
  width: 250px;
  margin-right: 15px;
}

.infoAboutFilm-name {
  text-align: center;
}

.infoAboutFilm-nameEn,
.infoAboutFilm-nameOR {
  font-size: 16px;
  color: gray;
  text-align: center;
}
</style>
