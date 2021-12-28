<template>
    <div class="song">
        <div class="song-image">
            <img :src="details.poster" :alt="details.title">
        </div>
        <div class="song-title">{{ details.title }}</div>
        <div class="song-author">{{ details.author }}</div>
        <div class="song-date">{{ details.year }}</div>
    </div>
</template>
<script>
export default {
    name: 'SongCard',
    props: {
        details: Object
    }
}
</script>
<style scoped>
.song {
    background-color: #2e3a46;
    width: calc(90% / 5);
    height: 350px;
    margin: 15px;
    padding: 25px;
    text-align: center;
    color: #5d6d74;
}
.song-title {
    color: white;
    margin: 10px 0;
}
.song-image {
    width: 150px;
}
</style>