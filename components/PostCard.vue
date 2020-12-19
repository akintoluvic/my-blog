<template>
    <nuxt-link
    :to="{ name: 'username-article', params: { username: article.user.username, article: article.id } }"
    tag="article"
     class="p-4 md:w-1/3"
  >
    <!-- <div> -->
        <div class="h-full border-2 border-gray-200 rounded-lg overflow-hidden">
          <img 
            class="lg:h-48 md:h-36 w-full object-cover object-center" 
            v-if="article.cover_image"
            :src="article.cover_image"
            :alt="article.title"
          >
          <img
           class="lg:h-48 md:h-36 w-full object-cover object-center" 
           v-else :src="article.social_image" :alt="article.title" />

          <div class="p-6">
            <!-- <h2 class="tracking-widest text-xs title-font font-medium text-gray-500 mb-1">CATEGORY</h2> -->
            <nuxt-link :to="{name: 'username-article', params: { username: article.user.username, article: article.id } }" >
                <h1 class="title-font text-lg font-medium text-gray-900 mb-3">{{ article.title }}</h1>
            </nuxt-link>
            <div class="flex flex-wrap mb-3">
                <nuxt-link
                    v-for="tag in article.tag_list"
                    :key="tag"
                    :to="{ name: 't-tag', params: { tag } }"
                    class="mr-1 mb-1 py-1 px-3 bg-gray-300 text-gray-700 rounded-lg"
                >
          #{{ tag }}
        </nuxt-link>
        </div>
            
            
            <div class="flex items-center flex-wrap ">
              <span class="text-gray-600 inline-flex items-center leading-none text-sm mr-2">
                <svg class="w-4 h-4 mr-1" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round" viewBox="0 0 24 24">
                  <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"></path>
                  <circle cx="12" cy="12" r="3"></circle>
                </svg>
                {{ article.positive_reactions_count }}
              </span>
              <span class="text-gray-600 inline-flex items-center leading-none text-sm">
                <svg class="w-4 h-4 mr-1" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round" viewBox="0 0 24 24">
                  <path d="M21 11.5a8.38 8.38 0 01-.9 3.8 8.5 8.5 0 01-7.6 4.7 8.38 8.38 0 01-3.8-.9L3 21l1.9-5.7a8.38 8.38 0 01-.9-3.8 8.5 8.5 0 014.7-7.6 8.38 8.38 0 013.8-.9h.5a8.48 8.48 0 018 8v.5z"></path>
                </svg>
                {{ article.comments_count }}
              </span>

              <span class="text-gray-600 mr-3 inline-flex items-center lg:ml-auto md:ml-0 ml-auto leading-none text-sm pr-3 py-1 border-r-2 border-gray-300">
                {{ article.readable_publish_date }}
              </span>
            </div>
          </div>
        </div>
      <!-- </div> -->
    </nuxt-link>
</template>

<script>
// import HeartIcon from '@/assets/icons/heart.svg?inline'
// import CommentsIcon from '@/assets/icons/comments.svg?inline'

export default {
    components: {
    //   HeartIcon,
    //   CommentsIcon
    },
    props: {
      article: {
        type: Object,
        default: null
      }
    },
}
</script>