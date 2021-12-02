<template>
    <div id="app">
        <Header
            @searchString="callAxios"
        />
        <main>
            <MoviesContainer
                :moviesApiResponse="moviesApiResponse"
                :seriesApiResponse="seriesApiResponse"
            />
        </main>
    </div>
</template>

<script>
import Header from './components/Header.vue'
import MoviesContainer from './components/MoviesContainer.vue'
import axios from 'axios'

export default {
    name: 'App',
    components: {
      Header,
      MoviesContainer
    },
    data() {
        return {
            moviesApiResponse: [],
            seriesApiResponse: []
        }
    },
    methods: {
        callAxios(stringToSearch) {

            axios
            .get(`https://api.themoviedb.org/3/search/movie?api_key=f98ea4f4b78ab3a6de36168ebf417712&language=it-IT&query=${stringToSearch}`)
            .then(response => {
                this.moviesApiResponse = response.data.results;
                console.log(this.moviesApiResponse);
            });

            axios
            .get(`https://api.themoviedb.org/3/search/tv?api_key=f98ea4f4b78ab3a6de36168ebf417712&language=it-IT&query=${stringToSearch}`)
            .then(response => {
                this.seriesApiResponse = response.data.results;
                console.log(this.seriesApiResponse);
            });
        }
    }
}
</script>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
</style>
