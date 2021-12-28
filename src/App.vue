<template>
  <div id="app">
    <Header/>
    <SongCardsList/>
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
};
</script>

<style lang="scss">

</style>
