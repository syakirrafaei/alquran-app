<template>
  <transition name="home">
    <div>
      <div class="fixed md:relative w-full md:flex md:pt-4">
        <div class="relative w-full md:w-1/4 text-center mx-auto">
          <input
            v-model="search"
            type="text"
            class="text-center px-3 py-3 md:rounded-lg shadow-sm w-full mb-10 dark:bg-gray-900"
            placeholder="Search for surah.."
          />
          <div class="absolute top-0 left-0 mt-3 ml-4">
            <svg
              class="w-6 h-6 text-gray-400"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
              ></path>
            </svg>
          </div>
        </div>
      </div>
      <div
        class="grid md:grid-cols-3 gap-4 md:px-64 lg:px-32 pt-20 md:pt-6 px-3 pb-20"
      >
        <div v-for="surah in filteredSurah" :key="surah.number">
          <nuxt-link :to="`/surah/${surah.number}`">
            <div
              class="bg-white dark:bg-gray-900 border dark:border-green-500 text-center rounded-lg shadow"
            >
              <div class="grid grid-cols-5">
                <div class="col-span-1 h-full hero rounded-tl-lg rounded-bl-lg">
                  <div
                    class="font-bold text-white bg-green-900 py-1 rounded-tl-lg"
                  >
                    Surah
                  </div>
                  <div class="font-bold text-white text-xl py-4">
                    {{ surah.number }}
                  </div>
                </div>
                <div class="col-span-4 p-6 dark:text-white">
                  <div class="text-lg font-bold md:mb-2">
                    {{ surah.englishNameTranslation }}
                  </div>
                  <div class="font-kitab">
                    {{ surah.name }}
                  </div>
                  <span class="text-base">( {{ surah.englishName }} )</span>
                </div>
              </div>
            </div>
          </nuxt-link>
        </div>
      </div>
    </div>
  </transition>
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
      const appendText = 'surah '
      return this.surahs.filter((surah) => {
        const concatSurah = appendText.concat(surah.number)
        return (
          surah.englishName.toLowerCase().includes(this.search.toLowerCase()) ||
          surah.englishNameTranslation
            .toLowerCase()
            .includes(this.search.toLowerCase()) ||
          surah.number
            .toString()
            .toLowerCase()
            .includes(this.search.toLowerCase()) ||
          concatSurah.includes(this.search.toLowerCase())
        )
      })
    },
  },
  transition: 'home',
}
</script>
<style>
.hero {
  background-color: #48bb78;
  background-image: url("data:image/svg+xml,%3Csvg width='48' height='64' viewBox='0 0 48 64' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M48 28v-4L36 12 24 24 12 12 0 24v4l4 4-4 4v4l12 12 12-12 12 12 12-12v-4l-4-4 4-4zM8 32l-6-6 10-10 10 10-6 6 6 6-10 10L2 38l6-6zm12 0l4-4 4 4-4 4-4-4zm12 0l-6-6 10-10 10 10-6 6 6 6-10 10-10-10 6-6zM0 16L10 6 4 0h4l4 4 4-4h4l-6 6 10 10L34 6l-6-6h4l4 4 4-4h4l-6 6 10 10v4L36 8 24 20 12 8 0 20v-4zm0 32l10 10-6 6h4l4-4 4 4h4l-6-6 10-10 10 10-6 6h4l4-4 4 4h4l-6-6 10-10v-4L36 56 24 44 12 56 0 44v4z' fill='%233ca175' fill-opacity='0.4' fill-rule='evenodd'/%3E%3C/svg%3E");
}
.text-upright {
  writing-mode: vertical-lr;
  text-orientation: upright;
}
.grid {
  align-items: center;
}
.home-enter-active,
.home-leave-active {
  transition: opacity 0.2s;
}
.home-enter,
.home-leave-active {
  opacity: 0;
}
</style>
