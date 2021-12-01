<template>
    <div class="movie">
        <div>Titolo: {{movieDetails.title}}</div>
        <div>Titolo originale: {{movieDetails.original_title}}</div>
        <div>Lingua: {{movieDetails.original_language}}</div>
        <div>Voto: {{movieDetails.vote_average}}</div>
    </div>
</template>

<script>
export default {
    name: 'Movie',
    props: {
        movieDetails: Object
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.movie {
    width: 23%;
    margin: 0 2% 30px 0;
    height: 300px;
    background-color: lightgreen;
}
</style>
