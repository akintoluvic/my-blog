<template>
      <nav class="bg-gray-100 shadow-lg">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-16">
        <div class="flex items-center">
          <div class="flex-shrink-0">
            <!-- <img class="h-8 w-8" src="https://tailwindui.com/img/logos/workflow-mark-indigo-500.svg" alt="Workflow"> -->
            <a href="/" class="text-xl leading-tight text-gray-700">
                Nuxt Dev.to
            </a>
          </div>
          
        </div>
            <div class="">
                <div class="ml-10 flex items-baseline space-x-4">
                <!-- Current: "bg-gray-900 text-white", Default: "text-gray-300 hover:bg-gray-700 hover:text-white" -->
                <a href="/" class="bg-gray-900 text-white px-3 py-2 rounded-md text-sm font-medium">New</a>

                <a href="/top" class="text-gray-600 hover:bg-gray-700 hover:text-white px-3 py-2 rounded-md text-sm font-medium">Top</a>

                <nuxt-link
                  v-for="tag in tags"
                  :key="tag"
                  class="text-gray-600 hover:bg-gray-700 hover:text-white px-3 py-2 rounded-md text-sm font-medium"
                  :to="{ name: 't-tag', params: {tag} }"
                >
                  {{tag}}
                </nuxt-link>

                </div>
            </div>
        </div>
    </div>
  </nav>

</template>
<script>
export default {
  data() {
    return {
      tags: [
        '#career',
        '#discuss',
      ]
    }
  },
}
</script>