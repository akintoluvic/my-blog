<template>
  <div class="mt-5">
    <div class="flex space-x-8">
      <article-block class="w-2/3 rounded-lg overflow-hidden" />
      <div class="w-1/3">
        <aside-username-block class="w-full bg-white rounded-lg overflow-hidden" />
      </div>
    </div>
    <comments-block class="comments-block" />
  </div>
</template>

<script>
  import ArticleBlock from '@/components/blocks/ArticleBlock'
  import CommentsBlock from '@/components/blocks/CommentsBlock'
  import AsideUsernameBlock from '@/components/blocks/AsideUsernameBlock'

  export default {
    components: {
      ArticleBlock,
      CommentsBlock,
      AsideUsernameBlock
    },
    


  }
</script>
