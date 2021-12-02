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
            seriesApiResponse: [],
        }
    },
    methods: {
        callAxios(stringToSearch) {

            axios
            .get(`https://api.themoviedb.org/3/search/movie?api_key=f98ea4f4b78ab3a6de36168ebf417712&language=it-IT&query=${stringToSearch}`)
            .then(response => {

                this.moviesApiResponse = response.data.results;
                console.log(this.moviesApiResponse);

                // una volta popolato l'array con i film trovati, invoco la funzione per chiedere la lista degli attori
                this.searchCast();
            });

            axios
            .get(`https://api.themoviedb.org/3/search/tv?api_key=f98ea4f4b78ab3a6de36168ebf417712&language=it-IT&query=${stringToSearch}`)
            .then(response => {
                this.seriesApiResponse = response.data.results;
                console.log(this.seriesApiResponse);
            });
        },
        searchCast() {
            this.moviesApiResponse.forEach(movie => {
                
                axios
                .get(`https://api.themoviedb.org/3/movie/${movie.id}/credits?api_key=f98ea4f4b78ab3a6de36168ebf417712`)
                .then(response => {

                    let movieToUpdate = this.moviesApiResponse.find(film => {
                        return film.id === response.data.id
                    });
                    movieToUpdate.castList = response.data.cast;
                    // movie.castList = response.data.cast;
                }); 

                console.log("array di film con cast aggiunto:", this.moviesApiResponse);
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
