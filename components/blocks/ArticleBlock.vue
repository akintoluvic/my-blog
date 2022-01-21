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
        <div v-if="article.cover_image" class="image-wrapper">
          <img :src="article.cover_image" class="rounded-lg" :alt="article.title" />
        </div>
        <div class="meta">
          <div class="scl">
            <span>
              <!-- <heart-icon /> -->
              {{ article.positive_reactions_count }}
            </span>
            <span class="comments" @click="scrollToComments">
              <!-- <comments-icon /> -->
              {{ article.comments_count }}
            </span>
          </div>
          <time>{{ article.readable_publish_date }}</time>
        </div>
      </header>
      <!-- eslint-disable-next-line -->
      <!-- <div class="content" v-html="article.body_html" v-pre >

      </div> -->
      <!-- <pre class="mx-4">{{article.body_html}}</pre> -->
      <div class="content px-5" v-html="article.body_html" />
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
