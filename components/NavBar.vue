<template>
  <div
    :class="{
      scrolled: !view.atTopOfPage,
    }"
    class="hidden md:block fixed bg-white w-full mt-0 top-0 nav shadow-sm"
  >
    <nav
      :class="{ scrolled: !view.atTopOfPage }"
      class="flex w-full items-center justify-between flex-wrap container mx-auto py-6 px-12 text-black"
    >
      <div class="flex items-center flex-no-shrink mr-6">
        <!-- <img src="~assets/Logo.svg" alt="Logo" class="h-12" /> -->
        <span class="font-bold italic text-xl"
          >Mudah<span class="text-green-500">Quran</span></span
        >
      </div>
      <div class="block sm:hidden">
        <button class="flex items-center px-3 py-2 rounded" @click="toggle">
          <svg
            class="fill-current h-6 w-6"
            viewBox="0 0 20 20"
            xmlns="http://www.w3.org/2000/svg"
          >
            <title>Menu</title>
            <path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z" />
          </svg>
        </button>
      </div>
      <div
        :class="open ? 'block' : 'hidden'"
        class="w-full flex-grow sm:flex sm:items-center sm:w-auto"
      >
        <div class="mt-4 md:mt-0 ml-auto tracking-wider text-center">
          <nuxt-link class="px-2" to="/">Home</nuxt-link>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  data() {
    return {
      open: false,
      view: {
        atTopOfPage: true,
      },
    }
  },
  beforeMount() {
    window.addEventListener('scroll', this.handleScroll)
  },
  methods: {
    toggle() {
      this.open = !this.open
    },
    handleScroll() {
      // when the user scrolls, check the pageYOffset
      if (window.pageYOffset > 0) {
        // user is scrolled
        if (this.view.atTopOfPage) this.view.atTopOfPage = false
      } else if (!this.view.atTopOfPage) {
        this.view.atTopOfPage = true
        // user is at top of page
      }
    },
  },
}
</script>

<style scoped>
.nav {
  z-index: 100;
}
div.scrolled {
  @apply shadow-2xl;
  border-bottom: 0px;
  background: rgba(243, 243, 243, 0.3);
  backdrop-filter: blur(8px);
}
</style>
