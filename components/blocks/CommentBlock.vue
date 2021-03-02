<template>
  <li class="comment" :class="level !== 0 && 'reply'">
    <div class="card">
      <div class="profile">
        <nuxt-link
          :to="{
            name: 'username',
            params: { username: comment.user.username }
          }"
          class="inner-link"
        >
          <img :src="comment.user.profile_image_90" :alt="comment.user.name" />
          <span>{{ comment.user.name }}</span>
        </nuxt-link>
        <a
          v-if="comment.user.twitter_username"
          :href="`https://twitter.com/${comment.user.twitter_username}`"
          target="_blank"
        >twitter
          <!-- <twitter-icon /> -->
        </a>
        <a
          v-if="comment.user.github_username"
          :href="`https://github.com/${comment.user.github_username}`"
          target="_blank"
        >git
          <!-- <github-icon /> -->
        </a>
        <a
          v-if="comment.user.website_url"
          :href="comment.user.website_url"
          target="_blank"
          rel="nofollow noopener noreferrer"
        >ext-link
          <!-- <external-link-icon /> -->
        </a>
      </div>
      <!-- eslint-disable-next-line -->
      <div v-html="comment.body_html" class="html-content"></div>
    </div>
    <ul>
      <comment-block
        v-for="reply in comment.children"
        :key="reply.id_code"
        :comment="reply"
        :level="level + 1"
      />
    </ul>
  </li>
</template>

<script>
// import CommentBlock from '@/components/blocks/CommentBlock'
// import TwitterIcon from '~/assets/icons/twitter.svg?inline'
// import GithubIcon from '~/assets/icons/github.svg?inline'
// import ExternalLinkIcon from '~/assets/icons/external-link.svg?inline'

export default {
  name: 'CommentBlock',
  components: {
    // CommentBlock,
    // TwitterIcon,
    // GithubIcon,
    // ExternalLinkIcon
  },
  props: {
    comment: {
      type: Object,
      default: null
    },
    level: {
      type: Number,
      default: null
    }
  }
}
</script>

