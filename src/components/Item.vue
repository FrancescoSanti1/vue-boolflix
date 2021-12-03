<template>
    <div class="item" v-if="showItem && checkboxType">
        <img class="poster" :src="imagePath" :alt="`locandina ${title}`">
        <div class="item-infos">
            <div><span class="bold">Titolo</span>: {{title}}</div>
            <div v-if="originalTitle !== title"><span class="bold">Titolo originale</span>: {{originalTitle}}</div>
            <div class="flag"><span class="bold">Lingua</span>:
                <img :src="flagPath" :alt="language">
                {{language}}
            </div>
            <div>
                <span class="bold">Voto</span>:
                <div v-for="star in 5" :key="star" :class="activeStar(star)" class="star"></div>
            </div>
            <div>
                <span class="bold">Cast</span>:
                <span class="actor" v-for="actor in castToPrintOnPage" :key="actor">{{actor}}</span>
            </div>
            <div>
                <span class="bold">Genere</span>:
                <span class="genre" v-for="genre in genres" :key="genre.id">{{genre.name}}</span>
            </div>
            <div>
                <span class="bold">Trama</span>:
                {{textOverview}}
            </div>
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
        posterPath: String,
        textOverview: String,
        cast: Array,
        genres: Array,
        selectedGenres: Array,
        checkboxType: Boolean,
    },
    computed: {
        ratingStars() {
            return Math.ceil(this.rating / 2);
        },
        imagePath() {
            if(this.posterPath !== null) {
                return `https://image.tmdb.org/t/p/w342${this.posterPath}`;
            } else {
                return `https://unsplash.it/300/500?image=10`;
            }
        },
        flagPath() {
            if(this.language == "it" || this.language == "en") {
                return require(`@/assets/img/${this.language}.svg`);
            } else {
                return require(`@/assets/img/xx.svg`);
            }
        },
        castToPrintOnPage() {
            let newList = [];
            if(this.cast) {
                for(let i = 0; i < 5; i++) {
                    if (this.cast[i]) {
                        newList.push(this.cast[i].original_name);
                    }
                }
            }
            return newList;
        },
        showItem() {
            let foundItem = false;
            if(this.selectedGenres.length === 0) {
                return true;
            } else {
                this.selectedGenres.forEach(genre => {
                
                    let foundGenre = this.genres.find(elem => {
                        return elem.name === genre;
                    });

                    if(foundGenre) {
                        foundItem = true;
                    }
                });
                return foundItem;
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
    border: lightgray 1px solid;
    height: 500px;
    overflow: hidden;
    position: relative;

    &:hover {
        .item-infos {
            display: block;
        }
    }

    .poster {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    .item-infos {

        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        padding: 20px 5px 10px;
        background-color: rgba(0, 0, 0, 0.8);
        color: white;
        display: none;

        div {
            margin-bottom: 5px;
        }

        .bold {
            font-weight: bold;
        }

        .flag {
            img {
                height: 14px;
                vertical-align: middle;
            }
        }
    
        .star {
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

        .actor::after, .genre::after {
            content: ", ";
        }

        .actor:last-of-type::after, .genre:last-of-type::after {
            content: ".";
        }
    }  
}
</style>
