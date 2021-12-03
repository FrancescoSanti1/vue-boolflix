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
                // una volta popolato l'array con i film trovati, invoco la funzione per chiedere la lista degli attori
                this.searchMovieCastAndGenres();
            });

            axios
            .get(`https://api.themoviedb.org/3/search/tv?api_key=f98ea4f4b78ab3a6de36168ebf417712&language=it-IT&query=${stringToSearch}`)
            .then(response => {
                this.seriesApiResponse = response.data.results;
                // una volta popolato l'array con le serie tv trovate, invoco la funzione per chiedere la lista degli attori
                this.searchSeriesCastAndGenres();
            });
        },
        searchMovieCastAndGenres() {
            this.moviesApiResponse.forEach(movie => {
                // richiesta per avere il cast del film
                axios
                .get(`https://api.themoviedb.org/3/movie/${movie.id}/credits?api_key=f98ea4f4b78ab3a6de36168ebf417712`)
                .then(response => {
                    
                    // movie.castList = response.data.cast;
                    this.$set(movie, 'castList', response.data.cast);
                    //console.log(movie.title, movie.castList.map(item => item.original_name).join(', '));
                }); 

                // richiesta per avere i generi del film
                axios
                .get(`https://api.themoviedb.org/3/movie/${movie.id}?api_key=f98ea4f4b78ab3a6de36168ebf417712`)
                .then(response => {
                    
                    // movie.castList = response.data.cast;
                    this.$set(movie, 'genresList', response.data.genres);
                    //console.log(movie.title, movie.castList.map(item => item.original_name).join(', '));
                }); 
            });
        },
        searchSeriesCastAndGenres() {
            this.seriesApiResponse.forEach(series => {
                // richiesta per avere il cast della serie
                axios
                .get(`https://api.themoviedb.org/3/tv/${series.id}/credits?api_key=f98ea4f4b78ab3a6de36168ebf417712`)
                .then(response => {
                    this.$set(series, 'castList', response.data.cast);
                });

                // richiesta per avere i generi della serie
                axios
                .get(`https://api.themoviedb.org/3/tv/${series.id}?api_key=f98ea4f4b78ab3a6de36168ebf417712`)
                .then(response => {
                    
                    // movie.castList = response.data.cast;
                    this.$set(series, 'genresList', response.data.genres);
                    //console.log(movie.title, movie.castList.map(item => item.original_name).join(', '));
                }); 
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
