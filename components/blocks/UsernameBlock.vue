<template>
  <section>
    <template v-if="$fetchState.pending">
      <div class="image-wrapper loading">
        <content-placeholders>
          <content-placeholders-img />
        </content-placeholders>
      </div>
      <div class="content">
        <content-placeholders rounded>
          <content-placeholders-text :lines="3" />
        </content-placeholders>
      </div>
      <div class="info">
        <content-placeholders rounded>
          <content-placeholders-text :lines="3" />
        </content-placeholders>
      </div>
    </template>
    <!-- <template v-else-if="$fetchState.error">
      <inline-error-block :error="$fetchState.error" />
    </template> -->
    <template v-else>
      <main class="w-full bg-gray-200 flex items-center space-x-8 rounded-2xl shadow mt-5 mb-12 p-8">
        <div class="image-wrapper w-3/12">
          <img :src="user.profile_image" class="rounded-full" :alt="user.name" />
        </div>
        <div class="content w-6/12">
          <h1 class="text-5xl font-bold mb-5">{{ user.name }}</h1>
          <a
            :href="`https://dev.to/${user.username}`"
            target="_blank"
            rel="nofollow noopener noreferrer"
            class="bg-gray-500 hover:bg-gray-600 text-white font-semibold px-32 py-3 rounded-md text-sm font-medium"
          >
            Follow
          </a>
          <div v-if="user.summary" class="summary mt-5">{{ user.summary }}</div>
          <div class="links">
            <a
              v-if="user.twitter_username"
              :href="`https://twitter.com/${user.twitter_username}`"
              target="_blank"
            >
              twitter-icon
            </a>
            <a
              v-if="user.github_username"
              :href="`https://github.com/${user.github_username}`"
              target="_blank"
            >
              github-icon
            </a>
            <a
              v-if="user.website_url"
              :href="user.website_url"
              target="_blank"
              rel="nofollow noopener noreferrer"
            >
              external-link-icon
            </a>
          </div>
        </div>

        <div class="info w-3/12">
          <div v-if="user.location">
            <div class="uppercase font-semibold text-sm text-gray-400">location</div>
            <div class="content">{{ user.location }}</div>
          </div>
          <div v-if="user.joined_at">
            <div class="uppercase font-semibold text-sm text-gray-400 mt-4">joined</div>
            <div class="content">{{ user.joined_at }}</div>
          </div>
        </div>
      </main>
    </template>
  </section>
</template>

<script>
// import InlineErrorBlock from '@/components/blocks/InlineErrorBlock'

export default {
  components: {
    // InlineErrorBlock
  },
  props: [],
  async fetch() {
    const res = await fetch(
      `https://dev.to/api/users/by_username?url=${this.$route.params.username}`
    )

    if (!res.ok) {
      // set status code on server
      if (process.server) {
        this.$nuxt.context.res.statusCode = 404
      }
      throw new Error('User not found')
    }
    this.user = await res.json()
  },
  data() {
    return {
      user: {}
    }
  },
  head() {
    return {
      title: this.user.name
    }
  }
}
</script>
