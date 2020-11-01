<template>
  <div class="md:px-64 pb-20">
    <div class="font-bold text-white text-4xl py-8 hero text-center">
      {{ ayahs.englishName }}
      <button
        v-if="showMalay === true"
        class="translation font-semibold block mx-auto text-base bg-green-600 shadow-lg rounded-lg px-3 py-1"
        @click="showMalay = !showMalay"
      >
        Hide Malay
      </button>
      <button
        v-else-if="showMalay === false"
        class="translation font-semibold block mx-auto text-base bg-green-600 shadow-lg rounded-lg px-3 py-1"
        @click="showMalay = !showMalay"
      >
        Show Malay
      </button>
    </div>
    <div
      v-for="ayah in ayahs.ayahs"
      :key="ayah.number"
      class="grid shadow bg-grey grid-rows-2 grid-cols-4 grid-flow-col"
    >
      <div class="row-span-2 col-span-1 text-center my-auto px-2">
        <div class="number-kitab rounded-full">
          {{ ayah.numberInSurah.toLocaleString('ar-EG') }}
        </div>
      </div>
      <!-- <div class="row-span-1 col-span-1 text-center"></div> -->
      <div class="row-span-2 col-span-3 text-right py-6 pl-1 pr-3 md:px-3">
        <span v-if="ayah.numberInSurah !== 1" class="inline-block font-kitab">
          <Highlight :ayah="ayah.text" />
          <div v-if="showMalay" class="text-sm italic">
            {{ ayahsMalay.ayahs[ayah.numberInSurah - 1].text }}
          </div>
        </span>
        <span
          v-else-if="ayah.numberInSurah === 1 && firstAyahs.length === 1"
          class="inline-block font-kitab"
        >
          <span>{{ firstAyahs }} بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ</span>
          <div v-if="showMalay" class="text-sm italic">
            {{ ayahsMalay.ayahs[ayah.numberInSurah - 1].text }}
          </div>
        </span>
        <span v-else class="inline-block font-kitab">
          <Highlight :ayah="firstAyahs" />
          <div v-if="showMalay" class="text-sm italic">
            {{ ayahsMalay.ayahs[ayah.numberInSurah - 1].text }}
          </div>
        </span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  async asyncData({ $axios, params }) {
    const res = await $axios.$get(`surah/${params.id}`)
    const resMalay = await $axios.$get(`surah/${params.id}/ms.basmeih`)
    const ayahs = res.data
    const ayahsMalay = resMalay.data
    return { ayahs, ayahsMalay }
  },
  data() {
    return {
      showMalay: true,
    }
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
.dark-mode .bg-grey:nth-child(even) {
  @apply bg-teal-800 text-white;
}
.dark-mode .bg-grey:nth-child(odd) {
  @apply text-white;
}
</style>
