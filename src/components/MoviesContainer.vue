<template>
    <div class="container">
        <div id="search">
            <input type="text" placeholder="scrivi qui cosa vuoi cercare...">
            <button>Cerca</button>
        </div>
        
        <div class="movies-container">
            <Movie/>
            <Movie/>
            <Movie/>
            <Movie/>
            <Movie/>
            <Movie/>
            <Movie/>
        </div>
    </div>
</template>

<script>
import Movie from '@/components/Movie.vue'

export default {
    name: 'MoviesContainer',
    components: {
        Movie
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
