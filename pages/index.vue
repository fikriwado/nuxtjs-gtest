<script setup>
const currentPage = ref(1)
const perPage = 5

const { data } = await useFetch('https://gorest.co.in/public/v2/posts/')

const posts = data.value
const startIndex = computed(() => (currentPage.value - 1) * perPage)
const endIndex = computed(() => currentPage.value * perPage)
const paginatedPosts = computed(() => posts.slice(startIndex.value, endIndex.value))
const totalPages = computed(() => Math.ceil(posts.length / perPage))
</script>

<template>
  <div class="space-y-3">
    <article
      v-for="post in paginatedPosts"
      :key="post.id"
      class="backdrop-blur-lg bg-slate-700/20 block gap-1 px-6 py-3 border border-white/10 rounded-lg w-full space-y-2"
    >
      <NuxtLink class="text-xl font-semibold" :to="{ name: 'posts-id', params: { id: post.id } }">{{ post.title }}</NuxtLink>
      <p class="text-slate-400 line-clamp-2">{{ post.body }}</p>
      <NuxtLink class="font-semibold inline-block" :to="{ name: 'posts-id', params: { id: post.id } }">Read more</NuxtLink>
    </article>

    <div class="flex justify-end mt-5">
      <button
        v-for="page in totalPages"
        :key="page"
        @click="currentPage = page"
        class="px-4 py-2 mx-1 rounded-lg backdrop-blur-lg bg-slate-700/20 border border-white/10"
        :class="{ 'bg-slate-700': currentPage === page }"
      >
        {{ page }}
      </button>
    </div>
  </div>
</template>
