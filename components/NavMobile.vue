<template>
  <div
    :class="{
      scrolled: !view.atTopOfPage,
    }"
    class="md:hidden fixed bg-white dark:bg-gray-800 w-full mt-0 bottom-0 nav shadow"
  >
    <nav
      :class="{ scrolled: !view.atTopOfPage }"
      class="w-full items-center justify-between grid grid-cols-3 py-1 px-3 text-center shadow"
    >
      <div class="col-span-1 focus:outline-none cursor-pointer">
        <color-mode />
      </div>
      <div class="col-span-1 focus:outline-none cursor-pointer">
        <nuxt-link class="focus:outline-none hover:bg-gray-200" to="/"
          ><svg
            class="w-6 h-6 mx-auto text-green-500"
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
          <div class="text-sm text-green-600 antialiased">Home</div>
        </nuxt-link>
      </div>
      <div class="col-span-1">
        <nuxt-link to="/belajar">
          <svg
            class="w-6 h-6 mx-auto text-green-500"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253"
            ></path>
          </svg>
          <div class="text-sm text-green-600 antialiased">Belajar</div>
        </nuxt-link>
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
</style>
