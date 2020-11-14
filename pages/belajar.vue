<template>
  <transition name="home">
    <div class="w-full md:w-1/2 mx-auto">
      <div
        class="w-full text-xl md:text-2xl hero p-6 md:p-8 font-bold text-white text-center"
      >
        Cara Belajar Memahami al-Quran
      </div>
      <div class="mx-4 mt-4 bg-green-600 p-3 font-bold text-white text-lg">
        <svg
          class="w-6 h-6 inline-block my-auto"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
          ></path>
        </svg>
        <span class="my-auto ml-2">Pengenalan</span>
      </div>
      <div
        class="text-white mx-4 mb-8 rounded-bl-lg rounded-br-lg shadow-lg p-6 font-semibold bg-green-500"
      >
        Terdapat 4 warna yang digunakan dalam kaedah ini. Klik pada warna
        dibawah untuk lihat lebih lanjut.
      </div>

      <div class="grid grid-cols-4 gap-4 justify-items-center px-6 mb-8">
        <div
          :class="selected === 'green' ? 'border-2 border-white' : ''"
          class="cursor-pointer p-5 shadow-lg rounded-full bg-green-600"
          @click="selected = 'green'"
        ></div>
        <div
          :class="selected === 'red' ? 'border-2 border-white' : ''"
          class="cursor-pointer p-5 shadow-lg rounded-full bg-red-600"
          @click="selected = 'red'"
        ></div>
        <div
          :class="selected === 'blue' ? 'border-2 border-white' : ''"
          class="cursor-pointer p-5 shadow-lg rounded-full bg-blue-600"
          @click="selected = 'blue'"
        ></div>
        <div
          :class="selected === 'black' ? 'border-2 border-white' : ''"
          class="cursor-pointer p-5 shadow-lg rounded-full bg-black"
          @click="selected = 'black'"
        ></div>
      </div>
      <div v-if="selected === 'green'">
        <div class="text-center text-green-600 text-2xl font-bold">Hijau</div>
        <div class="px-6 text-center text-lg dark:text-white">
          <p>
            Perkataan dalam Al-Quran yang sama erti dengan Bahasa
            Malaysia/Indonesia.
          </p>
          <p class="mt-2 font-bold">Contohnya: Kitab - Allah</p>
        </div>
      </div>
      <div v-else-if="selected === 'red'">
        <div class="text-center text-red-600 text-2xl font-bold">Merah</div>
        <div class="px-6 text-center text-lg dark:text-white">
          <p>
            Kalimah atau Huruf yang umumnya berulang di dalam al-Quran.
            Mempunyai sekitar 70 perkataan dalam al-Quran.
          </p>
          <p class="mt-2 font-bold">Contohnya: Didalam - Itu</p>
        </div>
      </div>
      <div v-else-if="selected === 'blue'">
        <div class="text-center text-blue-600 text-2xl font-bold">Biru</div>
        <div class="px-6 text-center text-lg dark:text-white">
          <p>
            Kalimah atau Huruf yang mudah difahami maknanya kerana banyak
            berulang atau mempunyai kata pinjaman dari Bahasa Arab ke Bahasa
            Malaysia.
          </p>
          <p class="mt-2 font-bold">Contohnya: Ibadah - Rahmah</p>
          <li v-for="info in infos['Blue']" :key="info.id">
            {{ info.arabic }}
            -
            {{ info.malay }}
          </li>
        </div>
      </div>
      <div v-else-if="selected === 'black'">
        <div class="text-center text-black text-2xl font-bold">Hitam</div>
        <div class="px-6 text-center text-lg dark:text-white">
          <p>
            Kalimah atau Huruf yang sukar difahami maknanya (Perkataan-perkataan
            ini tidak perlu dihafal maknanya, hanya perlu merujuk kamus).
          </p>
          <p class="mt-2 font-bold">Contohnya: Keraguan - Sama</p>
        </div>
      </div>
    </div>
  </transition>
</template>
<script>
import axios from 'axios'
export default {
  async asyncData() {
    // const res = await $axios.$get(
    //   'http://127.0.0.1:8000/api/dictionary/category'
    // )
    // const infos = res.data
    // return { infos }
    let infos = ''
    await axios
      .get(`http://127.0.0.1:8000/api/dictionary/category`)
      .then((response) => (infos = response.data.data))
      .catch((e) => console.log(e))

    return { infos }
  },
  data() {
    return {
      selected: 'green',
    }
  },
  created() {},
}
</script>
