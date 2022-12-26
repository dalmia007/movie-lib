<template>
  <div class="flex flex-col justify-center items-center m-auto md:h-screen">
    <p class="my-10 text-lg font-semibold">{{ data.title }}</p>
    <FormulateForm v-model="movie" @submit="submit">
      <div class="mb-4">
        <FormulateInput
          v-model="data.rating"
          label="Rating"
          name="rating"
          input-class="border border-gray-400 rounded px-3 py-2 leading-none focus:border-green-500 outline-none border-box w-full"
          error-class="text-red-700 text-xs mb-1"
          label-class="font-semibold"
          type="text"
          validation="number|max:100|min:1"
        />
      </div>

      <div class="mb-4">
        <FormulateInput
          id="director"
          v-model="data.director"
          label="Director"
          name="director"
          input-class="border border-gray-400 rounded px-3 py-2 leading-none focus:border-green-500 outline-none border-box w-full"
          error-class="text-red-700 text-xs mb-1"
          label-class="font-semibold"
          type="text"
          validation="required"
        />
      </div>
      <div class="mb-4">
        <FormulateInput
          id="date"
          v-model="data.releaseDate"
          name="releaseDate"
          label="Release Date"
          input-class="border border-gray-400 rounded px-3 py-2 leading-none focus:border-green-500 outline-none border-box w-full"
          error-class="text-red-700 text-xs mb-1"
          label-class="font-semibold"
          type="date"
          validation="date|required"
        />
      </div>
      <div class="mb-4">
        <FormulateInput
          id="synopsis"
          v-model="data.synopsis"
          name="synopsis"
          label="Synopsis"
          input-class="border border-gray-400 rounded px-3 py-2 leading-none focus:border-green-500 outline-none border-box w-full"
          error-class="text-red-700 text-xs mb-1"
          label-class="font-semibold"
          type="textarea"
          validation="required"
        />
      </div>
      <FormulateInput
        type="submit"
        label="Submit"
        class="px-2 bg-green-300 rounded max-w-max p-1"
      />
    </FormulateForm>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'EditMovie',
  data() {
    return {
      data: [],
      searchQuery: '',
      movie: {
        rating: '',
        director: '',
        releaseDate: '',
        synopsis: '',
      },
    }
  },
  created() {
    this.getMovieById()
  },
  methods: {
    async submit(): Promise<void> {
      try {
        const res = await this.$axios.put(
          `https://6395ab63a68e43e418ee1a13.mockapi.io/movies/${this.$route.params.id}`,
          {
            rating: this.movie.rating,
            director: this.movie.director,
            releaseDate: this.movie.releaseDate,
            synopsis: this.movie.synopsis,
          }
        )
        if (res.status === 200) {
          this.$router.go(-1)
        }
      } catch (err) {
        console.log(err)
      }
    },
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
