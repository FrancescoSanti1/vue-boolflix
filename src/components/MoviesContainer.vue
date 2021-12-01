<template>
    <div class="container">
        <div id="search">
            <input v-model="stringToSearch" @focus="stringToSearch = ''" type="text" placeholder="scrivi qui cosa vuoi cercare...">
            <button @click="searchMovies">Cerca</button>
        </div>
        
        <div class="movies-container">
            <Movie
                v-for="movie, i in apiResponse"
                :key="i"
                :movieDetails="movie"
            />
        </div>
    </div>
</template>

<script>
import Movie from '@/components/Movie.vue'
import axios from 'axios'

export default {
    name: 'MoviesContainer',
    components: {
        Movie
    },
    data() {
        return {
            stringToSearch: "",
            apiResponse: []
        }
    },
    methods: {
        searchMovies() {
            axios
            .get(`https://api.themoviedb.org/3/search/movie?api_key=f98ea4f4b78ab3a6de36168ebf417712&language=it-IT&query=${this.stringToSearch}`)
            .then(response => {
                this.apiResponse = response.data.results;
                console.log(this.apiResponse);
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
