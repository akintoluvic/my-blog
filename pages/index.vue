<template>
  
  <main class="w-full text-gray-700 body-font">
      <div v-if="$fetchState.pending" class="flex flex-wrap -m-4">
        <content-placeholders 
          v-for="p in 30"
          :key="p"
          rounded
          class="md:w-full"
        >
          <content-placeholders-img />
          <content-placeholders-text :lines="3" />
        </content-placeholders>
      </div>
      <div v-else-if="$fetchState.error">
        <p>{{ $fetchState.error.message }}</p>
      </div>
      <div v-else class="flex flex-wrap -m-4">
        <PostCard 
          v-for="(article, i) in articles"
          :key="article.id"
          :article="article"
          v-observe-visibility="
            i === articles.length - 1 ? lazyLoadArticles : false
          "
        />
      </div>
      <div v-if="$fetchState.pending && articles.length" class="flex flex-wrap -m-4">
        <content-placeholders 
          v-for="p in 30"
          :key="p"
          rounded
          class="md:w-full"
        >
          <content-placeholders-img />
          <content-placeholders-text :lines="3" />
        </content-placeholders>
      </div>
  </main>

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
        `https://dev.to/api/articles?tag=nuxt&state=rising&page=${this.currentPage}`
      ).then(res => res.json())
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