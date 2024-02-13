<script setup>
const route = useRoute()
const postId = route.params.id
const postsAPI = `https://gorest.co.in/public/v2/posts/${postId}`
const { data: post } = await useFetch(postsAPI)
const { data: commentsPost } = await useFetch(`${postsAPI}/comments`)
import { IconArrowNarrowLeft } from '@tabler/icons-vue'
</script>
<template>
  <button class="flex items-center py-2 pr-3 gap-1 mb-3" @click="$router.back()">
    <IconArrowNarrowLeft class="w-6 h-6" /> Back
  </button>
  <article>
    <h1 class="text-3xl md:text-5xl mb-7">{{ post.title }}</h1>
    <p class="text-justify">{{ post.body }}</p>
  </article>
  <div class="mt-7 space-y-3">
    <h3 class="text-xl">Comments ({{ commentsPost.length }})</h3>
    <div
      v-for="comment in commentsPost"
      :key="comment.id"
      class="backdrop-blur-lg bg-slate-700/20 block gap-1 px-4 py-3 border border-white/10 rounded-lg w-full space-y-2"
    >
      <div class="leading-none">
        <p>
          <span class="font-medium">{{ comment.name }}</span> -
          <span class="text-sm text-slate-400">{{ comment.email }}</span>
        </p>
      </div>
      <p class="">"{{ comment.body }}"</p>
    </div>
  </div>
</template>
