<template>
  <article>
    <template v-if="$fetchState.pending">
      <content-placeholders rounded>
        <content-placeholders-heading />
        <content-placeholders-img />
        <content-placeholders-text :lines="50" />
      </content-placeholders>
    </template>
    <!-- <template v-else-if="$fetchState.error">
      <inline-error-block :error="$fetchState.error" />
    </template> -->
    <template v-else>
      <header>
        <h1 class="text-4xl font-extrabold text-gray-800 mb-3">{{ article.title }}</h1>
        <div class="tags flex space-x-3 mb-8">
          <nuxt-link
            v-for="tag in article.tags"
            :key="tag"
            :to="{ name: 't-tag', params: { tag } }"
            class="tag px-3 py-1 bg-gray-400 rounded-md"
          >
            #{{ tag }}
          </nuxt-link>
        </div>
        <div v-if="article.cover_image" class="mb-5">
          <img :src="article.cover_image" class="rounded-lg" :alt="article.title" />
        </div>
        <div class="mb-10 flex justify-between">
          <div class="flex space-x-4">
            <span class="flex space-x-1">
              <!-- <heart-icon /> -->
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-red-700" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M3.172 5.172a4 4 0 015.656 0L10 6.343l1.172-1.171a4 4 0 115.656 5.656L10 17.657l-6.828-6.829a4 4 0 010-5.656z" clip-rule="evenodd" />
              </svg>
              <span>{{ article.positive_reactions_count || 0 }}</span>
            </span>
            <span class="flex space-x-1" @click="scrollToComments">
              <!-- <comments-icon /> -->
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
              </svg>
              <span>{{ article.comments_count || 0 }}</span>
            </span>
          </div>
          <time>{{ article.readable_publish_date }}</time>
        </div>
      </header>
      <!-- eslint-disable-next-line -->
      <!-- <div class="content" v-html="article.body_html" v-pre >

      </div> -->
      <!-- <pre class="mx-4">{{article.body_html}}</pre> -->
      <div class="article-body text-xl" v-html="article.body_html" />
    </template>
  </article>
</template>
<script>
// import InlineErrorBlock from '@/components/blocks/InlineErrorBlock'

export default {
  components: {
    // HeartIcon,
    // InlineErrorBlock,
    // CommentsIcon
  },
  props: [],
  async fetch() {
    const article = await fetch(
      `https://dev.to/api/articles/${this.$route.params.article}`
    ).then((res) => res.json())

    if (article.id && article.user.username === this.$route.params.username) {
      this.article = article
      this.$store.commit('SET_CURRENT_ARTICLE', this.article)
    } else {
      // set status code on server
      if (process.server) {
        this.$nuxt.context.res.statusCode = 404
      }
      throw new Error('Article not found')
    }
  },
  data() {
    return {
      article: {}
    }
  },
  activated() {
    // Call fetch again if last fetch more than 60 sec ago
    if (this.$fetchState.timestamp <= Date.now() - 60000) {
      this.$fetch()
    }
  },
  methods: {
    scrollToComments() {
      const el = document.querySelector('#comments')
      if (el) {
        const scrollTo = el.getBoundingClientRect().top
        window.scrollBy({ top: scrollTo - 20, left: 0, behavior: 'smooth' })
      }
    }
  },
  head() {
    return {
      title: this.article.title
    }
  }
}
</script>
<style scoped>
  /* Not working */
  .article-body li {
    @apply mb-5;
  }
</style>
