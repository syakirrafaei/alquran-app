<template>
  <div>
    <client-only placeholder="Loading...">
      <div class="flex flex-row flex-wrap" v-if="isLoading">
        <div class="w-full text-right mb-2">
          <svg
            class="inline-block animate-spin h-8 w-8 rounded-full border-t-4 border-green-500 mr-3 ..."
            viewBox="0 0 24 24"
          ></svg>
          <div class="text-base text-gray-600 font-semibold">Loading..</div>
        </div>
      </div>
      <span v-html="high"></span>
    </client-only>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  props: {
    ayah: {
      type: String,
      default: '',
    },
  },

  data() {
    return {
      high: '',
      info: '',
      isLoading: true,
    }
  },
  async mounted() {
    await axios
      .get(`https://admin.aridzuan.com/api/dictionary`)
      .then((response) => (this.info = response.data.data))
      .catch((e) => console.log(e))
      .finally(() => {
        this.high = this.ayah
        this.highlight()
      })
  },
  methods: {
    highlight() {
      for (const value of this.info) {
        if (value.color_name === 'Red') {
          this.high = this.high.replaceAll(
            value.arabic,
            `<span class="red">${value.arabic}</span>`
          )
        } else {
          this.high = this.high.replaceAll(
            value.arabic,
            `<span style="color: ${value.color};">${value.arabic}</span>`
          )
        }
      }
      this.isLoading = false
    },
  },
}
</script>
<style>
.red:nth-child(even) {
  @apply text-red-600;
}
.red:nth-child(odd) {
  @apply text-orange-500;
}
</style>
