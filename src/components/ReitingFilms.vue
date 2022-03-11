<template>
  <div @click="SortFilms" class="sortReit">Сортировать по рейтингу</div>
</template>

<script>
export default {
  name: "ReitingFilms",
  data() {
    return {
      isSort: false,
    };
  },
  methods: {
    SortFilms() {
      this.isSort ? (this.isSort = false) : (this.isSort = true);
      this.$emit("sort-films", { flagSort: this.isSort });
    },
  },
};
</script>

<style>
.sortReit {
  cursor: pointer;
}
</style>