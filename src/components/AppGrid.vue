<template>
    <section>
        <h2 class="m-0">{{items.length != 0 ? what : ''}}</h2>
        <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-4 gy-4">
            <div class="col" v-for="item in items" :key="item.id">
                <app-card :card="item"/>
            </div>
        </div>
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

<style lang="scss" scoped>
    h2{
        font-size: 45px;
        color: white;
        font-weight: 600;
        padding: 20px 0 10px 0;
    }
</style>