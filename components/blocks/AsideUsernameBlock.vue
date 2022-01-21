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
          <img :src="user.profile_image" class="w-full rounded-lg" :alt="user.name" />
        </nuxt-link>
        <div class="my-4">
          <nuxt-link
            :to="{
              name: 'username',
              params: { username: user.username }
            }"
            class="block text-gray-800 font-semibold text-2xl"
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
        class="bg-gray-300 rounded-lg py-4 text-center w-full block"
      >
        See profile
      </nuxt-link>
      <div class="flex flex-col space-y-4 mt-4">
        <div v-if="user.summary">
          <span class="text-gray-700">About: </span>
          <span class="content">{{ user.summary }}</span>
        </div>
        <div v-if="user.location">
          <span class="text-gray-700">Location: </span>
          <span class="content">{{ user.location }}</span>
        </div>
        <div v-if="user.joined_at">
          <span class="text-gray-700">Joined: </span>
          <span class="content">{{ user.joined_at }}</span>
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

