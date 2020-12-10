<template>
  <div>
    <NavBar />
    <div class="min-h-screen md:mt-16 bg-gray-100 dark:bg-teal-900 antialiased">
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
.tooltip {
  position: relative; /* making the .tooltip span a container for the tooltip text */
}
.tooltip:before {
  content: attr(data-text); /* here's the magic */
  position: absolute;
  font-size: 16px;

  /* vertically center */
  bottom: 100%;
  transform: translateX(-50%);

  /* move to right */
  left: 50%;
  margin-top: 15px; /* and add a small left margin */

  /* basic styles */
  min-width: 100px;
  padding: 10px;
  border-radius: 10px;
  background: #000;
  color: #fff;
  text-align: center;
  z-index: 100;
  display: none; /* hide by default */
  opacity: 100;
  transition: 0.3s opacity;
}
.tooltip:hover:before {
  display: block;
}
.tooltip:after {
  content: '';
  position: absolute;

  /* position tooltip correctly */
  top: 50%;
  margin-top: -35px;

  /* vertically center */
  left: 50%;
  transform: translateX(-50%);

  /* the arrow */
  border: 10px solid #000;
  border-color: black transparent transparent transparent;

  display: none;
  opacity: 0;
  transition: 0.3s;
}
.tooltip:hover:before,
.tooltip:hover:after {
  display: block;
}

.tooltip:hover:after {
  display: block;
  opacity: 1;
}
</style>
