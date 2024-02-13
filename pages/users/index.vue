<script setup>
import { IconPlus } from '@tabler/icons-vue'
definePageMeta({
  layout: 'users'
})
const tableHead = ['No', 'Name', 'Email', 'Gender', 'Status', 'Action']
const { data: users } = await useFetch('https://gorest.co.in/public/v2/users/')
const classesDataHead =
  'border-b border-slate-100 dark:border-slate-700 text-slate-300 p-2'
</script>
<template>
  <div class="space-y-3">
    <NuxtLink
      :to="{ name: 'users-create' }"
      class="inline-flex items-center gap-1 transition duration-300 cursor-pointer py-2 px-3 bg-slate-700 border border-slate-200/10 hover:bg-slate-800 rounded"
    >
      <IconPlus class="w-5 h-5" />
      Add Users
    </NuxtLink>
    <table
      class="table-auto w-full bg-slate-700/20 border border-slate-200/20 rounded-lg text-slate-500"
    >
      <thead>
        <tr>
          <th
            v-for="(head, i) in tableHead"
            :key="i"
            :class="[
              classesDataHead,
              { 'w-16': i == 0, 'w-24': i == 3 || i == 4 }
            ]"
          >
            {{ head }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, i) in users" :key="user.id">
          <td :class="classesDataHead" class="text-center">{{ i + 1 }}</td>
          <td :class="classesDataHead">{{ user.name }}</td>
          <td :class="classesDataHead">{{ user.email }}</td>
          <td :class="classesDataHead" class="text-center">
            {{ user.gender }}
          </td>
          <td :class="classesDataHead" class="text-center">
            {{ user.status }}
          </td>
          <td :class="classesDataHead" class="text-center space-x-2">
            <NuxtLink
              class="transition duration-300 cursor-pointer inline-block py-0.5 px-2 bg-slate-700 border border-slate-200/10 hover:bg-slate-800 rounded"
              >Edit</NuxtLink
            >
            <NuxtLink
              class="transition duration-300 cursor-pointer inline-block py-0.5 px-2 bg-slate-700 border border-slate-200/10 hover:bg-slate-800 rounded"
              >Delete</NuxtLink
            >
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
