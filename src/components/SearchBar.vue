<template>
    <div>
        <input type="text" v-model="searchTxt" @keyup.enter="search">
        <button @click="search">Cerca</button>
    </div>
</template>

<script>

export default {
    name: 'SearchBar',
    data() {
        return {
            searchTxt: ''
        }
    },
    methods: {
        search() {
            this.$emit('search', this.searchTxt)
        }
    }
}
</script>

<style lang="scss">

</style>