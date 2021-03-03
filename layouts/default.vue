<template>
    <div class="w-full bg-gray-100">
      <Navbar />
      <div class="max-w-7xl mx-auto py-4 px-4 sm:px-6 lg:px-8">
        <Nuxt keep-alive />
      </div>
      
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
