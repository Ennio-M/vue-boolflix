<template>
    <div class="input-group" @click="search">
        <span class="input-group-text">
            <i class="fa-solid fa-magnifying-glass"></i>
        </span>
        <input type="text" class="form-control" placeholder="Cerca un film o una serie tv..." v-model="searchTxt" @keyup.enter="search">
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
    .input-group{
        width: 300px !important;
    }
</style>