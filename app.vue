<template>
  <div class="bg-black">
    <div class="bg-violet-900/20 text-slate-200 min-h-screen flex justify-center pt-20 pb-28 antialiased tracking-tight">
      <NuxtLoadingIndicator :throttle="0" />
      <NuxtLayout>
        <NuxtPage />
      </NuxtLayout>
    </div>
  </div>
</template>
