<template>
    <header>
        <img class="logo" src="../assets/logo-small.svg" alt="">
        <label for="genre">Genere</label>
        <select v-model="selectedGenre" id="genre" @change="emitFiltersValues()">
            <option value="">Tutti i generi</option>
            <option v-for="(genre, index) in genres" :key="index" :value="genre">{{ genre }}</option>
        </select>
    </header>
</template>
<script>
export default {
    name: "Header",
    props: {
        genres: Array,
    },
    data: function() {
        return {
            selectedGenre: '',
        };
    },
    methods: {
        emitFiltersValues: function() {
            this.$emit('selectChanged', {
                selectedGenre: this.selectedGenre,
            });
        }
    }
}
</script>
<style scoped>
header {
    background-color: #2e3a46;
}
.logo {
    width: 5%;
    padding: 15px;
    height: 70px;
    color: white;
}
select {
    min-width: 250px;
    margin: 0 20px;
    padding: 5px;
}
</style>