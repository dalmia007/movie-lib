<template>
  <div class="flex flex-col justify-center items-center m-auto md:h-screen">
    <MovieBanner v-if="data.length" :movies="data" />
    <h1 v-else>There are no movies in the database</h1>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import MovieBanner from '~/components/MovieBanner.vue'

export default Vue.extend({
  name: 'IndexPage',
  components: {
    MovieBanner,
  },
  data() {
    return {
      data: [],
      searchQuery: '',
    }
  },
  created() {
    this.getMovies()
  },
  methods: {
    getMovies(): void {
      this.$axios
        .get(`https://6395ab63a68e43e418ee1a13.mockapi.io/movies`)
        .then((res) => {
          this.data = res.data
        })
        .catch((e) => {
          console.error(e)
        })
    },
  },
})
</script>
