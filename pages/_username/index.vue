<template>
  <div class="page-wrapper">
    <username-block />
    <main class="max-w-2xl mx-auto text-gray-700 body-font">
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
    </main>
  </div>
</template>

<script>
import UsernameBlock from '../../components/blocks/UsernameBlock.vue'

export default {
  components: { UsernameBlock },
  async fetch() {
    const res = await fetch(
      // eslint-disable-next-line
      `https://dev.to/api/articles?username=${this.$route.params.username}`
    )
    // eslint-disable-next-line
    this.articles = await res.json()
  },
  data() {
    return {
      articles: null
    }
  }
}
</script>
