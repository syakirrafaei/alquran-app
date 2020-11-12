<template>
  <div
    :class="{
      scrolled: !view.atTopOfPage,
    }"
    class="hidden md:block fixed dark:bg-teal-800 bg-white w-full mt-0 top-0 nav shadow-sm"
  >
    <nav
      :class="{ scrolled: !view.atTopOfPage }"
      class="flex w-full items-center justify-between flex-wrap container mx-auto py-3 px-12 text-black"
    >
      <div class="flex items-center flex-no-shrink mr-6">
        <!-- <img src="~assets/Logo.svg" alt="Logo" class="h-12" /> -->
        <span class="font-bold italic text-xl dark:text-white"
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
        <div class="mt-4 md:mt-0 ml-auto text-center">
          <div class="cursor-pointer inline-block">
            <nuxt-link to="/">
              <svg
                class="text-green-500 w-6 h-6 mx-auto"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"
                ></path>
              </svg>
            </nuxt-link>
            <span class="text-green-600 px-2 antialiased text-sm">Home</span>
          </div>
          <div class="cursor-pointer inline-block"><color-mode /></div>
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
  background: #1c3f42;
  backdrop-filter: blur(8px);
}
</style>
