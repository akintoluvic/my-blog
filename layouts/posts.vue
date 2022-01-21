<template>
  <div class="bg-gray-100">
  <Navbar />
  <header class="w-full h-auto">
    <div class="max-w-6xl mx-auto py-4 px-4 sm:px-6 lg:px-8 ">
      <p class="text-base font-bold leading-tight text-gray-900">
        Categories
      </p>
    </div>
  </header>
  
  <main class="text-gray-700 body-font">
    <div class="max-w-6xl mx-auto flex space-x-8 px-8 pt-4 pb-24 mx-auto">
      <div class="w-1/4 -mt-4">
        <div class="bg-white p-4 rounded-xl">
          <h3>Popular Tags</h3>
          <nuxt-link
              v-for="tag in tags"
              :key="tag"
              :to="{ name: 't-tag', params: { tag } }"
              class="block mt-3"
            >
              {{ tag }}
            </nuxt-link>
        </div>
      </div>
      <div class=" w-2/4 flex flex-wrap">
        <Nuxt keep-alive />
      </div>
      <div class="w-1/4 h-screen -m-4">
        <div class="bg-gray-300 rounded-lg w-full rounded-xl p-4">
          <h3 class="text-xl mb-3 text-gray-800 font-semibold">DEV.to Re-immagined by Akintunde Victor on Nuxt using dev.to API</h3>
          <p>We're a place where coders share, stay up-to-date and grow their careers.</p>
          <nuxt-link
              class="block mt-4 w-full text-center py-2 bg-gray-900 text-white rounded-md"
              to=""
            >
              Opening Soon
            </nuxt-link>
        </div>
      </div>
    </div>
  </main>
</div>

</template>
<script>
export default {
  data() {
    return {
      tags: [
        '#javascript',
        '#webdev',
        '#beginners',
        '#programming',
        '#tutorial',
        '#react',
        '#python',
        '#productivity',
        '#css',
      ]
    }
  },
}
</script>

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
