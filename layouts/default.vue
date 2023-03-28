<template>
  <div>
    <header class="shadow-sm bg-white">
      <nav class="container mx-auto p-4 flex justify-between">
        <NuxtLink to="/" class="font-bold">Hacker News</NuxtLink>
        <ul class="flex gap-4">
          <li><NuxtLink to="/">Top</NuxtLink></li>
          <li><NuxtLink to="/new">New</NuxtLink></li>
          <li><NuxtLink to="/best">Best</NuxtLink></li>
          <li><NuxtLink to="/ask">Ask</NuxtLink></li>
          <li><NuxtLink to="/show">Show</NuxtLink></li>
          <li><NuxtLink to="/jobs">Jobs</NuxtLink></li>
        </ul>
      </nav>
    </header>
    <!-- output the page content -->
    <div class="container mx-auto p-4">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.router-link-exact-active {
  color: #12b488;
}
</style>
