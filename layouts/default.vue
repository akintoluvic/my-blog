<template>
  <div class="bg-gray-100">
  <Navbar />
  <header class="w-full h-auto">
    <div class="max-w-7xl mx-auto py-4 px-4 sm:px-6 lg:px-8 ">
      <p class="text-base font-bold leading-tight text-gray-900">
        Categories
      </p>
    </div>
  </header>
  
  <main class="text-gray-700 body-font">
    <div class="max-w-7xl mx-auto flex space-x-6 px-8 pt-4 pb-24 mx-auto">
      <div class="w-1/4 h-64 bg-gray-300 rounded-xl -mt-4">jjjj</div>
      <div class=" w-2/4 flex flex-wrap -m-4">
        <Nuxt keep-alive />
      </div>
      <div class="w-1/4 h-screen">
        <div class="bg-gray-300 rounded-lg h-48 w-full rounded-xl -mt-4">
          hjjj
        </div>
      </div>
    </div>
  </main>
</div>

</template>

<style>
/* .site-bg {
  @apply bg-gray-800 min-h-screen text-gray-100;
} */
html {
  font-family:
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}
</style>
