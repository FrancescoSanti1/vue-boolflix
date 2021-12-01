<template>
    <div class="container">
        <div id="search">
            <input v-model="stringToSearch" @focus="stringToSearch = ''" type="text" placeholder="scrivi qui cosa vuoi cercare...">
            <button @click="searchMovies">Cerca</button>
        </div>
        
        <div class="movies-container">
            <Item
                v-for="movie in moviesApiResponse"
                :key="movie.id"
                :title="movie.title"
                :originalTitle="movie.original_title"
                :language="movie.original_language"
                :rating="movie.vote_average"
            />

            <Item
                v-for="series in seriesApiResponse"
                :key="series.id"
                :title="series.name"
                :originalTitle="series.original_name"
                :language="series.original_language"
                :rating="series.vote_average"
            />
        </div>
    </div>
</template>

<script>
import Item from '@/components/Item.vue'
import axios from 'axios'

export default {
    name: 'MoviesContainer',
    components: {
        Item,
    },
    data() {
        return {
            stringToSearch: "",
            moviesApiResponse: [],
            seriesApiResponse: []
        }
    },
    methods: {
        searchMovies() {
            axios
            .get(`https://api.themoviedb.org/3/search/movie?api_key=f98ea4f4b78ab3a6de36168ebf417712&language=it-IT&query=${this.stringToSearch}`)
            .then(response => {
                this.moviesApiResponse = response.data.results;
                console.log(this.moviesApiResponse);
            });

            axios
            .get(`https://api.themoviedb.org/3/search/tv?api_key=f98ea4f4b78ab3a6de36168ebf417712&language=it-IT&query=${this.stringToSearch}`)
            .then(response => {
                this.seriesApiResponse = response.data.results;
                console.log(this.seriesApiResponse);
            });
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.container {
    min-height: calc(100vh - 80px);
    background-color: grey;

    #search {
        display: flex;
        justify-content: center;
        padding: 30px 0;

        input {
            width: 200px;
        }
    }

    .movies-container {
        width: 80%;
        margin: 0 auto;
        display: flex;
        flex-wrap: wrap;
        justify-content: flex-start;
    }
}

</style>
