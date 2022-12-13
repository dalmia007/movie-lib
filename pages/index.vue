<template>
  <div>
    {{ data }}
  </div>
  <!-- <Tutorial /> -->
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
  data() {
    return {
      data: null,
    }
  },
  mounted() {
    this.getMovies()
  },
  methods: {
    getMovies() {
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
