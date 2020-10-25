<template>
  <div class="md:px-64">
    <div class="font-bold text-4xl text-center mb-10">
      {{ ayahs.englishName }}
    </div>
    <div
      v-for="ayah in ayahs.ayahs"
      :key="ayah.number"
      class="grid shadow bg-grey grid-rows-2 grid-cols-4 grid-flow-col"
    >
      <div class="row-span-2 col-span-1 text-center my-auto">
        <div class="font-bold h-20 w-20 shadow py-4 rounded-full text-4xl">
          {{ ayah.numberInSurah.toLocaleString('ar-EG') }}
        </div>
      </div>
      <!-- <div class="row-span-1 col-span-1 text-center"></div> -->
      <div class="row-span-2 col-span-3 text-right py-6 px-1 md:px-3">
        <span v-if="ayah.numberInSurah !== 1" class="inline-block font-kitab">
          <Highlight :ayah="ayah.text" />
        </span>
        <span
          v-else-if="ayah.numberInSurah === 1 && firstAyahs.length === 1"
          class="inline-block font-kitab"
        >
          <span>{{ firstAyahs }} بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ</span>
        </span>
        <span v-else class="inline-block font-kitab">
          <Highlight :ayah="firstAyahs" />
        </span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  async asyncData({ $axios, params }) {
    const res = await $axios.$get(`surah/${params.id}`)
    const ayahs = res.data
    return { ayahs }
  },
  computed: {
    firstAyahs() {
      const ayahsFirst = this.ayahs.ayahs[0].text
      return ayahsFirst.replace('بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ', '')
    },
  },
}
</script>
<style>
.bg-grey:nth-child(even) {
  @apply bg-white;
}
</style>
