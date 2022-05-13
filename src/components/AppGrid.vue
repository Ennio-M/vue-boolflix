<template>
    <section>
        <h2>{{items.length != 0 ? what : ''}}</h2>
        <ul>
        <app-card  v-for="item in items" :key="item.id" :card="item"/>
      </ul>
    </section>
</template>

<script>
import AppCard from './AppCard.vue'

export default {
    name: 'AppGrid',
    components: {
        AppCard
    },
    props: {
        items: Array,
        what: String
    },
    data() {
        return {
            
        }
    },
    methods: {

    }
}
</script>

<style lang="scss">

</style>