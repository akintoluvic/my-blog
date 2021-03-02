<template>
  <aside>
    <template v-if="$fetchState.pending">
      <div class="username-heading loading">
        <content-placeholders>
          <content-placeholders-heading :img="true" />
        </content-placeholders>
      </div>
      <div class="info">
        <content-placeholders>
          <content-placeholders-text :lines="3" />
        </content-placeholders>
      </div>
    </template>
    <!-- <template v-else-if="$fetchState.error">
      <inline-error-block :error="$fetchState.error" />
    </template> -->
    <template v-else>
      <nuxt-link
        class="username-heading"
        :to="{
          name: 'username',
          params: { username: user.username }
        }"
        tag="div"
      >
        <nuxt-link
          :to="{
            name: 'username',
            params: { username: user.username }
          }"
        >
          <img :src="user.profile_image" :alt="user.name" />
        </nuxt-link>
        <div class="text">
          <nuxt-link
            :to="{
              name: 'username',
              params: { username: user.username }
            }"
          >
            <span>{{ user.name }}</span>
          </nuxt-link>
          <nuxt-link
            :to="{
              name: 'username',
              params: { username: user.username }
            }"
          >
            <span>@{{ user.username }}</span>
          </nuxt-link>
        </div>
      </nuxt-link>
      <nuxt-link
        :to="{
          name: 'username',
          params: { username: user.username }
        }"
        class="f-button"
      >
        See profile
      </nuxt-link>
      <div class="info">
        <div v-if="user.summary">
          <div class="title">about</div>
          <div class="content">{{ user.summary }}</div>
        </div>
        <div v-if="user.location">
          <div class="title">location</div>
          <div class="content">{{ user.location }}</div>
        </div>
        <div v-if="user.joined_at">
          <div class="title">joined</div>
          <div class="content">{{ user.joined_at }}</div>
        </div>
      </div>
    </template>
  </aside>
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
      throw new Error(`User ${this.$route.params.username} not found`)
    }
    this.user = await res.json()
  },
  fetchOnServer: false,
  data() {
    return {
      user: {}
    }
  }
}
</script>

