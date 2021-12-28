<template>
    <section>
        <div class="container">
            <div v-if="song.lenght > 0" class="row row-cols-2 row-cols-lg-4">
                <SongCard v-for="(element, index) in song.response" :key="index" :details="element"/>
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
    data: function() {
        return {
            songs: [],
        };
    },
    created: function() {
        axios.get('https://flynn.boolean.careers/exercises/api/array/music')
        .then((response) => {
            this.songs = response.data;
        });
    }

}
</script>
<style scoped>
@import '../style/containers.scss';
</style>