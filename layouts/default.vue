<template>
  <div>
    <NavBar />
    <div class="min-h-screen md:mt-20 bg-gray-100 dark:bg-teal-900 antialiased">
      <Nuxt />
    </div>
    <NavMobile />
  </div>
</template>
<style>
@font-face {
  font-family: 'Kitab';
  src: url('https://cdn.quranonline.net/wp-content/plugins/quran-learning-app/public/app/assets/fonts/UH1_Ver14.otf');
  /* src: url('//cdn.alquran.cloud/public/fonts/Kitab-Regular.ttf'); */
}

.font-kitab {
  font-family: 'Kitab';
}

@font-face {
  font-family: 'Kitab Bold';
  src: url('//cdn.alquran.cloud/public/fonts/Kitab-Bold.ttf');
}

.font-kitab-bold {
  font-family: 'Kitab Bold';
}
.font-kitab {
  font-family: 'Kitab';
  font-size: 40px;
}
.number-kitab {
  font-family: 'Kitab';
  font-size: 50px;
}
html.dark-mode {
  @apply bg-teal-900;
}
</style>
