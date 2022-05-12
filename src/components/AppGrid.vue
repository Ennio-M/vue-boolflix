<template>
    <section>
        <ul>
        <li v-for="movie in movies" :key="movie.id">
          id: {{movie.id}} <br>
          titolo originale: {{movie.original_title}} <br>
          titolo: {{movie.title}} <br>
          lingua: {{movie.original_language}} <br>
          voto: {{movie.vote_average}}
        </li>
      </ul>
    </section>
</template>

<script>

export default {
    name: 'AppGrid',
    props: {
        movies: Array
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