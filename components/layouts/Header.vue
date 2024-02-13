<template>
  <h1 class="text-center text-4xl font-semibold py-3 mb-8">Synapsis</h1>
  <nav
    class="fixed z-[1000] bottom-0 sm:bottom-[40px] left-1/2 -translate-x-1/2 flex items-center gap-1 px-6 py-3 backdrop-blur-lg border-t sm:border border-white/10 sm:rounded-lg w-full sm:w-fit justify-center"
  >
    <div class="relative flex items-center gap-2">
      <NuxtLink class="transition duration-300 rounded px-2 py-1 hover:bg-slate-100/10" :to="{ name: 'index' }">Home</NuxtLink>
      <NuxtLink class="transition duration-300 rounded px-2 py-1 hover:bg-slate-100/10" :to="{ name: 'about' }">About</NuxtLink>
    </div>
  </nav>
</template>
