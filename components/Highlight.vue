<template>
  <div>
    <client-only placeholder="Loading...">
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
    },
  },
}
</script>
<style>
.red:nth-child(even) {
  @apply text-red-600;
}
.red:nth-child(odd) {
  @apply text-orange-600;
}
</style>
