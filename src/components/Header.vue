<template>
    <header>
        <img class="logo" src="../assets/logo-small.svg" alt="">
        <label for="genre">Genere</label>
        <select v-model="selectedGenre" id="genre" @change="emitFiltersValues()">
            <option value="">Tutti i generi</option>
            <option v-for="(genre, index) in genres" :key="index" :value="genre">{{ genre }}</option>
        </select>

        <label for="author">Author</label>
        <select id="author" v-model="selectedAuthor" @change="emitFiltersValues()">
            <option value="">Tutti gli autori</option>
            <option v-for="(author, index) in authors" :key="index" :value="author">{{ author }}</option>
        </select>
    </header>
</template>
<script>
export default {
    name: "Header",
    props: {
        genres: Array,
        authors: Array
    },
    data: function() {
        return {
            selectedGenre: '',
            selectedAuthor: ''
        };
    },
    methods: {
        emitFiltersValues: function() {
            this.$emit('selectChanged', {
                selectedGenre: this.selectedGenre,
                selectedAuthor: this.selectedAuthor
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