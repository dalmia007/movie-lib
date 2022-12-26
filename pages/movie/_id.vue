<template>
  <div class="flex flex-col justify-center items-center m-auto md:h-screen">
    <div class="py-3 lg:max-w-[50%] sm:mx-auto">
      <div
        class="md:bg-white md:shadow-lg md:border-gray-100 md:border md:rounded-3xl p-8 flex space-x-8"
      >
        <div class="hidden md:block h-48 overflow-visible w-1/2">
          <img class="rounded-3xl shadow-lg" :src="data.poster" alt="" />
        </div>
        <div class="flex flex-col md:w-1/2 space-y-4">
          <div class="flex md:hidden h-72 overflow-visible w-3/4 mx-auto">
            <img class="rounded-3xl shadow-lg" :src="data.poster" alt="" />
          </div>
          <div class="flex justify-between items-start">
            <h2 class="text-2xl font-semibold">{{ data.title }}</h2>
          </div>
          <div>
            <div class="bg-yellow-400 max-w-max rounded-lg p-2 mb-1">
              {{ data.rating }}
            </div>
            <div class="text-lg mt-1">{{ data.director }}</div>
            <div class="text-lg">{{ data.releaseDate }}</div>
          </div>
          <p class="text-gray-400 md:max-h-40 overflow-y-scroll">
            {{ data.synopsis }}
          </p>
        </div>
      </div>
    </div>
  </div>
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
