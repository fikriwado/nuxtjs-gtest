<script setup>
import { IconArrowNarrowLeft } from '@tabler/icons-vue'

const forms = reactive({
  name: '',
  email: '',
  gender: 'male',
  status: 'active',
  newUser: {}
})

const handleSubmit = async (e) => {
  e.preventDefault()
  const { data } = await useFetch('https://gorest.co.in/public/v2/users/', {
    method: 'post',
    headers: {
      authorization:
        'Bearer 431a13a2b2a839abb281c0e7e81688c64d61b6b3f77c45dde3d1484eef689155'
    },
    body: {
      email: forms.email,
      name: forms.name,
      gender: forms.gender,
      status: forms.status
    },
    onResponse({ request, response, options }) {
      if (response.status == 201) {
        forms.name = ''
        forms.email = ''
        forms.gender = 'male'
        forms.status = 'active'
        forms.newUser = response._data
      }
    }
  })
}
</script>
<template>
  <NuxtLink
    :to="{ name: 'users' }"
    class="flex items-center py-2 pr-3 gap-1 mb-3"
  >
    <IconArrowNarrowLeft class="w-6 h-6" /> Back
  </NuxtLink>

  <p v-if="forms.newUser.name" class="mb-3 font-semibold text-teal-400">
    Success add new user: {{ forms.newUser.name }}
  </p>
  <form @submit="handleSubmit" class="space-y-4">
    <div class="space-y-1">
      <label for="" class="font-medium">Name</label>
      <input
        type="text"
        v-model="forms.name"
        class="w-full focus:outline-none focus:ring focus:ring-violet-200 focus:border-violet-400 border-vilet-300 shadow-sm rounded-lg transition duration-300 text-slate-900"
        placeholder="Enter name"
      />
    </div>
    <div class="space-y-1">
      <label for="" class="font-medium">Email</label>
      <input
        type="email"
        v-model="forms.email"
        class="w-full focus:outline-none focus:ring focus:ring-violet-200 focus:border-violet-400 border-vilet-300 shadow-sm rounded-lg transition duration-300 text-slate-900"
        placeholder="Enter name"
      />
    </div>
    <div class="space-y-1">
      <label for="" class="font-medium">Gender</label>
      <select
        v-model="forms.gender"
        class="w-full focus:outline-none focus:ring focus:ring-violet-200 focus:border-violet-400 border-vilet-300 shadow-sm rounded-lg transition duration-300 text-slate-900"
      >
        <option value="male">Male</option>
        <option value="female">Female</option>
      </select>
    </div>
    <div class="space-y-1">
      <label for="" class="font-medium">Status</label>
      <select
        v-model="forms.status"
        class="w-full focus:outline-none focus:ring focus:ring-violet-200 focus:border-violet-400 border-vilet-300 shadow-sm rounded-lg transition duration-300 text-slate-900"
      >
        <option value="active">Active</option>
        <option value="inactive">Inactive</option>
      </select>
    </div>

    <button
      type="submit"
      class="transition duration-300 cursor-pointer inline-block py-2 px-3 bg-slate-700 border border-slate-200/10 hover:bg-slate-800 rounded"
    >
      Submit
    </button>
  </form>
</template>
