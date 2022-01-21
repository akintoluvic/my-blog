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
  function capitalize(str) {
    return str.charAt(0).toUpperCase() + str.slice(1)
  }

  export default {
    layout: 'posts',
    data() {
      return {
        currentPage: 1,
        articles: [],
      }
    },
    async fetch() {
      const articles = await fetch(
        `https://dev.to/api/articles?tag=${this.$route.params.tag}&top=365&page=${this.currentPage}`
      ).then(res => res.json())
      if (!articles.length && this.currentPage === 1) {
        // set status code on server
        if (process.server) {
            this.$nuxt.context.res.statusCode = 404
        }
        throw new Error(`Tag ${this.$route.params.tag} not found`)
      }
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
      },
      head() {
        return {
        title:
            this.$route.params.tag &&
            `${capitalize(this.$route.params.tag)} articles`
        }
    }
    }
    
  }
</script>