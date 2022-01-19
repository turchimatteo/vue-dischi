<template>
  <div id="app">
    <Header @selectChanged="setFilters" :genres="genresList"/>
    <SongCardsList :filterGenre="selectedGenre"  @genresListCreated="setGenresList" />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import SongCardsList from "./components/SongCardsList.vue";

export default {
  name: "App",
  components: {
    Header,
    SongCardsList,
  },
  data: function() {
    return {
      selectedGenre: '',
      selectedAuthor: '',
      genresList: [],
    };
  },
  methods: {
    setFilters: function(filters) {
      this.selectedGenre = filters.selectedGenre;
    },
    setGenresList: function(genres) {
      this.genresList = genres;
    },
  }
};
</script>

<style lang="scss">


* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

img {
    max-width: 100%;
    display: block;
}

body {
    font-family: "Roboto", sans-serif;
}

.container {
    width: 70%;
    margin: auto;
}

#app {
    width: 100%;
    height: 100vh;
}
</style>
