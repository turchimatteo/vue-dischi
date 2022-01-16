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
        filterAuthor: String
    },
    data: function() {
        return {
            discsList: [],
            isLoadingApi: true,
            genresList: [],
            authorsList: []
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
                    if(!this.authorsList.includes(element.author)) {
                        this.authorsList.push(element.author);
                    }
                });
                this.$emit('genresListCreated', this.genresList);
                this.$emit('authorsListCreated', this.authorsList);
                this.isLoadingApi = false;
            });
        }
    },
    computed: {
        filteredDiscs: function() {
            if(this.filterGenre === '' && this.filterAuthor === '') {
                return this.discsList;
            }
            let filteredDiscs = this.discsList;
            if(this.filterGenre !== '') {
                filteredDiscs = filteredDiscs.filter((element) => {
                    return element.genre === this.filterGenre;
                });
            }
            if(this.filterAuthor !== '') {
                filteredDiscs = filteredDiscs.filter((element) => {
                    return element.author === this.filterAuthor;
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