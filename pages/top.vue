<template>
      <div class="flex flex-wrap -m-4">
        <!-- <PostCard2 /> -->
        
        <PostCard 
          v-for="(article, i) in articles"
          :key="article.id"
          :article="article"
          v-observe-visibility="
            i === articles.length - 1 ? lazyLoadArticles : false
          "
        />
        
      </div>

</template>

<script>
  export default {
    layout: 'posts',
    data() {
      return {
        currentPage: 1,
        articles: []
      }
    },
    async fetch() {
      const articles = await fetch(
        `https://dev.to/api/articles?tag=nuxt&top=365&page=${this.currentPage}`
      ).then(res => res.json())
      // console.log(articles)
      this.articles = this.articles.concat(articles)
    },
    methods: {
      lazyLoadArticles(isVisible) {
        if (isVisible) {
          if (this.currentPage < 5) {
            this.currentPage++
            this.$fetch()
          }
        }
      }
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
