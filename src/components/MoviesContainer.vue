<template>
    <div class="items-container">
        <Item
            :selectedGenres="selectedGenres"
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
            :checkboxType="showMovies"
        />

        <Item
            :selectedGenres="selectedGenres"
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
            :checkboxType="showSeries"
        />
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
        seriesApiResponse: Array,
        selectedGenres: Array,
        checkboxMovies: Boolean,
        checkboxSeries: Boolean
    },
    computed: {
        showMovies() {
            if(!this.checkboxMovies && !this.checkboxSeries) {
                return true;
            } else if(this.checkboxMovies) {
                return true;
            } else {
                return false;
            }
        },
        showSeries() {
            if(!this.checkboxMovies && !this.checkboxSeries) {
                return true;
            } else if(this.checkboxSeries) {
                return true;
            } else {
                return false;
            }
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.items-container {
    width: 80%;
    display: flex;
    flex-wrap: wrap;
    justify-content: flex-start;
}

</style>
