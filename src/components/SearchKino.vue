<template>
  <div class="search-menu flex">
    <input
      v-model="search"
      @input="ShowFilm"
      type="text"
      id="search"
      class="search-input"
      placeholder="Поиск по кинопоиску"
    />
    <SearchIcon class="icon-search" alt="search kino" />
  </div>
</template>

<script>
import SearchIcon from "./SearchIcon.vue";
export default {
  name: "SearchKino",
  data() {
    return {
      search: "",
    };
  },
  components: {
    SearchIcon,
  },
  methods: {
    ShowFilm() {
      this.$emit("search-kino", { search: this.search });
    },
  },
};
</script>

<style>
.search-menu {
  justify-content: center;
  margin-bottom: 15px;
}
.search-input {
  padding: 0;
  width: 400px;
  height: 35px;
  border-color: #2d527c;
  margin-right: 0;
}

.icon-search {
  cursor: pointer;
  padding: 2px;
  margin: 0;
  background-color: #2d527c;
  fill: aliceblue;
  height: 35px;
  width: 50px;
}
</style>

