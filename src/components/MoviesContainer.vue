<template>
    <div class="container">

        <div class="movies-container">
            <Item
                v-for="movie in moviesApiResponse"
                :key="movie.id"
                :title="movie.title"
                :originalTitle="movie.original_title"
                :language="movie.original_language"
                :rating="movie.vote_average"
                :posterPath="movie.poster_path"
                :textOverview="movie.overview"
                :cast="movie.castList"
                :genres="movie.genresList"
            />

            <Item
                v-for="series in seriesApiResponse"
                :key="series.id"
                :title="series.name"
                :originalTitle="series.original_name"
                :language="series.original_language"
                :rating="series.vote_average"
                :posterPath="series.poster_path"
                :textOverview="series.overview"
                :cast="series.castList"
                :genres="series.genresList"
            />
        </div>
    </div>
</template>

<script>
import Item from '@/components/Item.vue'

export default {
    name: 'MoviesContainer',
    components: {
        Item,
    },
    props: {
        moviesApiResponse: Array,
        seriesApiResponse: Array
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.container {
    min-height: calc(100vh - 80px);
    background-color: grey;
    padding: 30px 0;

    .movies-container {
        width: 80%;
        margin: 0 auto;
        display: flex;
        flex-wrap: wrap;
        justify-content: flex-start;
    }
}

</style>
