<template>
  <article>
    <template v-if="$fetchState.pending">
      <content-placeholders rounded>
        <content-placeholders-heading />
        <content-placeholders-img />
        <content-placeholders-text :lines="50" />
      </content-placeholders>
    </template>
    <template v-else-if="$fetchState.error">
      <inline-error-block :error="$fetchState.error" />
    </template>
    <template v-else>
      <header>
        <h1>{{ article.title }}</h1>
        <div class="tags">
          <nuxt-link
            v-for="tag in article.tags"
            :key="tag"
            :to="{ name: 't-tag', params: { tag } }"
            class="tag"
          >
            #{{ tag }}
          </nuxt-link>
        </div>
        <div v-if="article.cover_image" class="image-wrapper">
          <img :src="article.cover_image" :alt="article.title" />
        </div>
        <div class="meta">
          <div class="scl">
            <span>
              <heart-icon />
              {{ article.positive_reactions_count }}
            </span>
            <span class="comments" @click="scrollToComments">
              <comments-icon />
              {{ article.comments_count }}
            </span>
          </div>
          <time>{{ article.readable_publish_date }}</time>
        </div>
      </header>
      <!-- eslint-disable-next-line -->
      <div class="content" v-html="article.body_html" />
    </template>
  </article>
</template>
<script>
export default {
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
                // throwing an error will set $fetchState.error
                throw new Error('Article not found')
        }
    },
    activated() {
        if (this.$fetchState.timestamp <= Date.now() - 60000) {
        this.$fetch()
        }
    }
}
</script>