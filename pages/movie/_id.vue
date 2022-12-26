<template>
  <MovieDetail :data="data" />
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IdSlugPage',
  data() {
    return {
      data: [],
      searchQuery: '',
    }
  },
  created() {
    this.getMovieById()
  },
  methods: {
    getMovieById(): void {
      this.$axios
        .get(
          `https://6395ab63a68e43e418ee1a13.mockapi.io/movies/${this.$route.params.id}`
        )
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

<style scoped></style>
