<template>
    <div class="w-100 h-100 mycard overflow-hidden">
        <div v-if="card.poster_path != null" class="w-100 h-100">
            <img :src="imgUrl + imgWidth + card.poster_path" class="w-100 h-100">
        </div>
        <div class="w-100 h-100" v-else>
            <img :src="require('../assets/imgs/fallback.jpg')" alt="Generic poster" class="w-100 h-100">
        </div>
        <div class="description">
            <div>
                <h4 class="d-inline-block">Titolo:&nbsp;</h4> <span class="film_data">{{card.title ? card.title : card.name}}</span>
            </div>
            <div v-if="card.title != card.original_title || card.name != card.original_name">
                <h4 class="d-inline-block">Titolo originale:&nbsp;</h4> <span class="film_data">{{card.original_title ? card.original_title : card.original_name}}</span>
            </div>
            <div>
                <h4 class="d-inline-block">Lingua:&nbsp;</h4>
                <img :src="require(`../assets/flags/flagImgs/${flagCode}.png`)" :alt="flagCode + ' flag'">
            </div>
            <div>
                <h4 class="d-inline-block">Voto:&nbsp;</h4> <span v-if="card.vote_count > 0">
                    <i v-for="(n, i) in 5" :key="i" :class="n < transform(card.vote_average) ? 'fa-solid gold' : 'fa-regular'" class="fa-star"></i>
                </span>
                <span class="film_data" v-else>0 voti</span>
            </div>
            <div>
                <h4 class="d-inline-block">Trama:</h4> <br>
                <span class="film_data" v-if="card.overview">{{card.overview.slice(0, 200) + '...'}}</span>
                <span class="film_data" v-else>Trama non presente</span>
            </div>
        </div>
    </div>
</template>

<script>
import codes from '../assets/flags/codes.js';

export default {
    name: 'AppCard',
    data() {
        return {
            imgUrl: 'https://image.tmdb.org/t/p/',
            imgWidth: 'w342',
            flagCode: ''
        }
    },
    props: {
        card: Object
    },
    methods: {
        transform(vote) {
            return parseInt(vote / 2)
        }
    },
    created() {
        for(let i = 0; i < codes.length; i++) {
            if(codes[i].language === this.card.original_language) {
                this.flagCode = codes[i].countryCode
                return
            }
        }
        this.flagCode = this.card.original_language
    }
}
</script>

<style lang="scss" scoped>
    .gold{
        color: gold;
    }
    .mycard{
        position: relative;
        &:hover{
            border: 1px solid white;
            cursor: pointer;
        }
        &:hover .description{
            display: block;
        }
    }
    .description{
        position: absolute;
        z-index: 1000;
        color: white;
        top: 0;
        height: 100%;
        width: 100%;
        display: none;
        background-color: rgba($color: #000000, $alpha: 0.8);
        padding: 30px 15px;
        .film_data{
            font-size: .8em;
        }
    }
</style>