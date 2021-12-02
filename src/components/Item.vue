<template>
    <div class="item">
        <img class="poster" :src="`https://image.tmdb.org/t/p/w342${posterPath}`" :alt="`locandina ${title}`">
        <div>Titolo: {{title}}</div>
        <div>Titolo originale: {{originalTitle}}</div>
        <div class="flag">Lingua: 
            <img :src="imagePath" :alt="language">
            {{language}}
        </div>
        <div>Voto: 
            <div v-for="star in 5" :key="star" :class="activeStar(star)" class="circle"></div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Item',
    props: {
        title: String,
        originalTitle: String,
        language: String,
        rating: Number,
        posterPath: String
    },
    computed: {
        ratingStars() {
            return Math.ceil(this.rating / 2);
        },
        imagePath() {
            if(this.language == "it" || this.language == "en") {
                return require(`@/assets/img/${this.language}.svg`);
            } else {
                return require(`@/assets/img/xx.svg`);
            }
        }
    },
    methods: {
        activeStar(numero) {
            if(numero <= this.ratingStars) {
                return "active";
            } else {
                return "";
            }
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.item {
    width: 23%;
    margin: 0 2% 30px 0;
    // height: 300px;

    .poster {
        width: 100%;
    }

    .flag {
        img {
            height: 14px;
            vertical-align: middle;
        }
    }
    
    .circle {
        display: inline-block;
        height: 18px;
        width: 18px;
        clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
        vertical-align: middle;
        border-radius: 50%;
        margin: 0 2px;
        background-color: lightgrey;

        &.active {
            background-color: gold;
        }
    }
}
</style>
