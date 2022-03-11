<template>
  <li class="poster-film" @click="ShowModal">
    <div class="black-img">
      <img class="img-film" :src="CheckImage" :alt="films.nameRu" />
    </div>
  </li>
</template>

<script>
import ModalFilm from "./ModalFilm.vue";
export default {
  name: "CardFilms",
  props: {
    films: { type: Object },
  },

  methods: {
    ShowModal() {
      this.$modal.show(ModalFilm, { film: this.films, poster: this.CheckImage}, { height: "auto" });
    },
  },
  computed: {
    CheckImage() {
      return this.films.posterUrl
        ? this.films.posterUrl
        : this.films.posterUrlPreview;
    },
  },
};
</script>

<style>
.poster-film {
  cursor: pointer;
  width: 20%;
  margin: 0 20px 10px 0;
}
.img-film {
  height: 300px;
}
</style>