<template>
    <section>
        <div class="container">
            <div v-if="!isLoadingApi" class="discs-list">
                <SongCard v-for="(disc, index) in filteredDiscs" :key="index" :details="disc" />
            </div>
        </div>
    </section>
</template>
<script>
import axios from 'axios';
import SongCard from './SongCard';

export default {
    name: 'SongCardList',
    components: {
        SongCard
    },
    props: {
        filterGenre: String,
    },
    data: function() {
        return {
            discsList: [],
            isLoadingApi: true,
            genresList: [],
        };
    },
    methods: {
        getDiscs: function() {
            axios.get('https://flynn.boolean.careers/exercises/api/array/music')
            .then((response) => {
                this.discsList = response.data.response;
                this.discsList.forEach((element) => {
                    if(!this.genresList.includes(element.genre)) {
                       this.genresList.push(element.genre); 
                    }
                });
                this.$emit('genresListCreated', this.genresList);
                this.isLoadingApi = false;
            });
        }
    },
    computed: {
        filteredDiscs: function() {
            if(this.filterGenre === '') {
                return this.discsList;
            }
            let filteredDiscs = this.discsList;
            if(this.filterGenre !== '') {
                filteredDiscs = filteredDiscs.filter((element) => {
                    return element.genre === this.filterGenre;
                });
            }
            return filteredDiscs;
        }
    },
    created: function() {
        this.getDiscs();
    }

}
</script>
<style scoped lang="scss">
@import '../style/container.scss';
section {
    overflow-y: auto;
    padding: 40px 0;
    background-color: #1e2e3c;
    height: calc(100% - 70px);
    color: white;
    .discs-list {
        display: flex;
        flex-wrap: wrap;
    }
}
</style>