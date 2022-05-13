<template>
    <li>
        <div v-if="card.poster_path != null">
            <img :src="imgUrl + imgWidth + card.poster_path" :alt="card.original_title + ' poster'">
        </div>
        <div v-else>
            <h2>{{card.original_title ? card.original_title : card.original_name}}</h2>
        </div>
         <br>
        titolo originale: {{card.original_title ? card.original_title : card.original_name}} <br>
        titolo: {{card.title ? card.title : card.name}} <br>
        lingua: <img :src="require(`../assets/flags/flagImgs/${flagCode}.png`)" :alt="flagCode + ' flag'"> <br>
        voto: <span v-if="card.vote_count > 0">
            <i v-for="(n, i) in 5" :key="i" :class="n < transform(card.vote_average) ? 'fa-solid gold' : 'fa-regular'" class="fa-star"></i>
        </span>
        <span v-else>0 voti</span>
        
    </li>
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
</style>