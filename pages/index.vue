<template>
  <div>
    <div class="fixed md:relative w-full md:flex md:pt-4">
      <div class="w-full text-center">
        <input
          v-model="search"
          type="text"
          class="text-center px-3 py-3 md:rounded-lg shadow-sm border w-full md:w-1/4 mb-10"
          placeholder="Search for surah.."
        />
      </div>
    </div>
    <div
      class="grid md:grid-cols-3 gap-4 md:px-64 lg:px-32 pt-20 md:pt-6 px-3 pb-20"
    >
      <div v-for="surah in filteredSurah" :key="surah.number">
        <nuxt-link :to="`/surah/${surah.number}`">
          <div class="bg-white text-center rounded-lg shadow p-6 md:h-40">
            <div class="text-lg font-bold md:mb-2">
              Surah {{ surah.number }}
            </div>
            <div class="font-kitab">
              {{ surah.name }}
            </div>
            <span class="text-base">( {{ surah.englishName }} )</span>
          </div>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  async asyncData({ $axios }) {
    const res = await $axios.$get('/surah')
    const surahs = res.data
    return { surahs }
  },
  data() {
    return {
      search: '',
    }
  },
  computed: {
    filteredSurah() {
      return this.surahs.filter((surah) => {
        return surah.englishName
          .toLowerCase()
          .includes(this.search.toLowerCase())
      })
    },
  },
}
</script>
