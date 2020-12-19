<template>
<div>
  <Navbar />
  <header class="bg-white shadow">
    <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
      <h1 class="text-3xl font-bold leading-tight text-gray-900">
        Dashboard
      </h1>
    </div>
  </header>
  
  <main class="text-gray-700 body-font">
    <div class="container px-5 py-24 mx-auto">
      <div class="flex flex-wrap -m-4">
        <PostCard2 />
        
        <PostCard 
          v-for="article in articles"
          :key="article.id"
          :article="article"
        />
        
      </div>
    </div>
  </main>
</div>

</template>

<script>
export default {
  data() {
      return {
        currentPage: 1,
        articles: []
      }
    },
    async fetch() {
      const articles = await fetch(
        `https://dev.to/api/articles?tag=nuxt&state=rising&page=${this.currentPage}`
      ).then(res => res.json())
      // console.log(articles)
      this.articles = this.articles.concat(articles)
    }
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/

</style>
