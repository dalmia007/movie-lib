<template>
  <div class="bg-white container mx-auto flex flex-wrap justify-center">
    <div v-for="movie in movies" :key="movie.id">
      <n-link :to="`/movie/${movie.id}`">
        <div
          class="rounded shadow-lg overflow-hidden m-2 transition duration-325 transform hover:-translate-y-1 hover:-translate-x-1 hover:scale-101 w-[300px] text-center"
        >
          <img :src="movie.poster" class="movie-image" />
          <p>Release: {{ movie.releaseDate }}</p>
          <p>Rating: {{ movie.rating }}</p>
        </div>
      </n-link>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: 'MovieBanner',
  props: {
    movies: { default: null, type: Array },
  },
}
</script>

<style>
.movie-image {
  width: 100%;
  height: 400px;
}
</style>
