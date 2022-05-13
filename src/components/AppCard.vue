<template>
    <li>
        titolo originale: {{card.original_title ? card.original_title : card.original_name}} <br>
        titolo: {{card.title ? card.title : card.name}} <br>
        lingua: <img :src="require('../flags/flagImgs/' + flagCode + '.png')" :alt="flagCode + ' flag'"> <br>
        voto: {{card.vote_average}}
    </li>
</template>

<script>
//import flags from '../flags/flags.js'

export default {
    name: 'AppCard',
    data() {
        return {
            
        }
    },
    props: {
        card: Object
    },
    computed: {
        flagCode() {
            if(this.card.original_language === 'en') {
                return 'gb'
            } else{
                return this.card.original_language
            }
        }
    }
}
</script>

<style lang="scss" scoped>

</style>