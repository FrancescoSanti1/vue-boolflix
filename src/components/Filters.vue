<template>
    <aside>
        <ul>
            <h3>Filtra per tipo</h3>
            <li>
                <input type="checkbox" id="checkMovies" v-model="showMovies" @change="$emit('checkMovies', showMovies)">
                <label for="checkMovies">Film</label>
            </li>
            <li>
                <input type="checkbox" id="checkSeries" v-model="showSeries" @change="$emit('checkSeries', showSeries)">
                <label for="checkSeries">Serie tv</label>
            </li>
        </ul>
        <ul>
            <h3>Filtra per generi</h3>
            <li v-for="genre in mergedGenresList" :key="genre.id">
                <input type="checkbox" :id="genre.id" :value="genre.name" v-model="checkedGenres" @change="$emit('sendGenres', checkedGenres)">
                <label :for="genre.id">{{genre.name}}</label>
            </li>
        </ul>
    </aside>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Filters',
    data() {
        return {
            movieGenresList: [],
            seriesGenresList: [],
            checkedGenres: [],
            showMovies: false,
            showSeries: false
        }
    },
    computed: {
        mergedGenresList() {
            let mergedList = [];
            mergedList = this.movieGenresList.slice();

            this.seriesGenresList.forEach(genre => {
                
                let foundGenre = mergedList.find(elem => {
                    return elem.name === genre.name;
                });

                if(!foundGenre) {
                    mergedList.push(genre);
                }
            });
            return mergedList;
        }
    },
    created() {
        // richiedo al server la lista dei generi per i film
        axios
        .get(`https://api.themoviedb.org/3/genre/movie/list?api_key=f98ea4f4b78ab3a6de36168ebf417712`)
        .then(response => {
            this.movieGenresList = response.data.genres
        });

        // richiedo al server la lista dei generi per le serie tv
        axios
        .get(`https://api.themoviedb.org/3/genre/tv/list?api_key=f98ea4f4b78ab3a6de36168ebf417712`)
        .then(response => {
            this.seriesGenresList = response.data.genres
        });
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

aside {
    width: 15%;
    padding: 0 10px;

    ul {
        list-style-type: none;

        li {
            margin: 3px 0;

            label {
                margin-left: 5px;
            }
        }
    }
}


</style>
