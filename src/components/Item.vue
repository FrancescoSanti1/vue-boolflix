<template>
    <div class="item">
        <!-- <img src="" alt=""> -->
        <div>Titolo: {{title}}</div>
        <div>Titolo originale: {{originalTitle}}</div>
        <div class="flag">Lingua: <img :src="require(`@/assets/img/${language}.svg`)" :alt="language"></div>
        <div>Voto: {{rating}}</div>
    </div>
</template>

<script>
export default {
    name: 'Item',
    props: {
        title: String,
        originalTitle: String,
        language: String,
        rating: Number
    },
    // computed: {
    //     imagePath() {
    //         if(this.movieDetails.original_language == "it" || this.movieDetails.original_language == "en") {
    //             return require(`@/assets/img/${this.movieDetails.original_language}.svg`);
    //         } else {
    //             return require(`@/assets/img/xx.svg`);
    //         }
    //     }
    // }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.item {
    width: 23%;
    margin: 0 2% 30px 0;
    height: 300px;
    background-color: lightgreen;

    .flag {
        img {
            height: 14px;
            vertical-align: middle;
        }
    }
    
}
</style>
