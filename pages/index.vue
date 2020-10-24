<template>
  <div class="grid md:grid-cols-3 gap-4 md:px-64">
    <div v-for="surah in surahs" :key="surah.number">
      <nuxt-link :to="`/surah/${surah.number}`">
        <div class="bg-white text-center rounded-lg shadow p-6 md:h-40">
          <div class="text-lg font-bold md:mb-2">Surah {{ surah.number }}</div>
          <div class="font-kitab">
            {{ surah.name }}
          </div>
          <span class="text-base">( {{ surah.englishName }} )</span>
        </div>
      </nuxt-link>
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
}
</script>
