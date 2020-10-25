<template>
  <div
    :class="{
      scrolled: !view.atTopOfPage,
    }"
    class="md:hidden fixed bg-white w-full mt-0 bottom-0 nav shadow"
  >
    <nav
      :class="{ scrolled: !view.atTopOfPage }"
      class="w-full items-center justify-between grid grid-cols-3 py-1 px-3 text-center shadow"
    >
      <div class="col-span-1"></div>
      <div class="col-span-1">
        <nuxt-link to="/"
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
      <div class="col-span-1"></div>
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
</style>
