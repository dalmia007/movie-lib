<template>
  <div
    class="data-image bg-cover hover:opacity-75"
    :style="{ backgroundImage: `url(${data})` }"
  />
</template>

<script lang="ts">
export default {
  name: 'MovieImage',
  props: {
    data: { default: '', type: String },
  },
  created() {
    console.log(this.data)
  },
}
</script>

<style>
.data-image {
  width: 100%;
  height: 400px;
}
</style>
