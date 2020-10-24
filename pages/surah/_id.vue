<template>
  <div class="md:px-64">
    <div class="font-bold text-4xl text-center mb-10">
      {{ ayahs.englishName }}
    </div>
    <ul v-for="ayah in ayahs.ayahs" :key="ayah.number" class="text-right">
      <span
        class="text-2xl rounded-full px-3 py-1 text-green-500 border-green-600 border text-center"
        >{{ ayah.numberInSurah }}</span
      >
      <li class="inline-block font-kitab mb-10">
        {{ ayah.text }}
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  async asyncData({ $axios, params }) {
    const res = await $axios.$get(`surah/${params.id}`)
    const ayahs = res.data
    return { ayahs }
  },
}
</script>
