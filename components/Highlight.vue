<template>
  <div>
    <client-only placeholder="Loading...">
      <span v-html="high"></span>
    </client-only>
  </div>
</template>
<script>
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
    }
  },
  beforeMount() {
    this.highlight()
  },
  methods: {
    highlight() {
      const myArray = [
        'الْحَمْدُ',
        'asdasdsfff',
        'مَالِكِ',
        'asdasds',
        'الْحَمْدُ',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'نَعْبُدُ',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'الْمُسْتَقِيمَ',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'الْعَالَمِينَ',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'الْمُفْلِحُونَ',
        'asdasds',
        'asdasds',
        'asdasds',
        'إِنَّ',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'asdasds',
        'صِرَاطَ',
      ]
      //   let buffer = this.high
      for (const value of myArray) {
        this.ayah = this.ayah.replaceAll(
          value,
          `<span class="text-blue-500">${value}</span>`
        )
      }
      this.high = this.ayah
    },
  },
}
</script>
