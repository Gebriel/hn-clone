<template>
  <div>
    <header class="header">
      <!-- <nav class="mx-auto p-4 bg-slate-100 flex justify-between">
        <div class="flex justify-center gap-3">
          <NuxtLink to="/"
            ><img class="h-7 w-7" src="~/assets/hacker-news-black-white.svg"
          /></NuxtLink>
          <NuxtLink
            to="/"
            class="font-bold text-lg text-gray-800 hidden md:block"
            >Hacker News</NuxtLink
          >
        </div>
        <ul class="flex gap-4">
          <li><NuxtLink to="/">Top</NuxtLink></li>
          <li><NuxtLink to="/new">New</NuxtLink></li>
          <li><NuxtLink to="/best">Best</NuxtLink></li>
          <li><NuxtLink to="/ask">Ask</NuxtLink></li>
          <li><NuxtLink to="/show">Show</NuxtLink></li>
          <li><NuxtLink to="/jobs">Jobs</NuxtLink></li>
        </ul>
      </nav> -->
      <nav class="mx-auto w-full p-6 shadow-sm">
        <div class="flex items-center justify-between">
          <!-- Header logo -->
          <div>
            <HackerNews />
          </div>

          <!-- Mobile toggle -->
          <div class="md:hidden">
            <button @click="drawer">
              <svg
                class="h-8 w-8 fill-current text-black"
                fill="none"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path d="M4 6h16M4 12h16M4 18h16"></path>
              </svg>
            </button>
          </div>

          <!-- Navbar -->
          <div class="hidden md:block">
            <ul class="flex space-x-8 text-sm font-sans">
              <li><NuxtLink to="/">Top</NuxtLink></li>
              <li><NuxtLink to="/new">New</NuxtLink></li>
              <li><NuxtLink to="/best">Best</NuxtLink></li>
              <li><NuxtLink to="/ask">Ask</NuxtLink></li>
              <li><NuxtLink to="/show">Show</NuxtLink></li>
              <li><NuxtLink to="/jobs">Jobs</NuxtLink></li>
              <!-- <li>
                <a
                  href="#"
                  class="cta bg-blue-500 hover:bg-blue-600 px-3 py-2 rounded text-white font-semibold"
                  >Sign Up</a
                >
              </li> -->
            </ul>
          </div>

          <!-- Dark Background Transition -->
          <transition
            enter-class="opacity-0"
            enter-active-class="ease-out transition-medium"
            enter-to-class="opacity-100"
            leave-class="opacity-100"
            leave-active-class="ease-out transition-medium"
            leave-to-class="opacity-0"
          >
            <div
              @keydown.esc="isOpen = false"
              v-show="isOpen"
              class="z-10 fixed inset-0 transition-opacity"
            >
              <div
                @click="isOpen = false"
                class="absolute inset-0 bg-black opacity-50"
                tabindex="0"
              ></div>
            </div>
          </transition>

          <!-- Drawer Menu -->
          <aside
            class="p-5 transform top-0 left-0 w-64 bg-white fixed h-full overflow-auto ease-in-out transition-all duration-300 z-30"
            :class="isOpen ? 'translate-x-0' : '-translate-x-full'"
          >
            <div class="close">
              <button
                class="absolute top-0 right-0 mt-4 mr-4"
                @click="isOpen = false"
              >
                <svg
                  class="w-6 h-6"
                  fill="none"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                >
                  <path d="M6 18L18 6M6 6l12 12"></path>
                </svg>
              </button>
            </div>

            <span
              @click="isOpen = false"
              class="flex w-full items-center pb-4 border-b"
            >
              <HackerNews />
            </span>

            <ul class="divide-y font-sans">
              <li>
                <NuxtLink
                  to="/"
                  @click="isOpen = false"
                  class="my-4 inline-block"
                  >Top</NuxtLink
                >
              </li>
              <li>
                <NuxtLink
                  to="/new"
                  @click="isOpen = false"
                  class="my-4 inline-block"
                  >New</NuxtLink
                >
              </li>
              <li>
                <NuxtLink
                  to="/best"
                  @click="isOpen = false"
                  class="my-4 inline-block"
                  >Best</NuxtLink
                >
              </li>
              <li>
                <NuxtLink
                  to="/ask"
                  @click="isOpen = false"
                  class="my-4 inline-block"
                  >Ask</NuxtLink
                >
              </li>
              <li>
                <NuxtLink
                  to="/show"
                  @click="isOpen = false"
                  class="my-4 inline-block"
                  >Show</NuxtLink
                >
              </li>
              <li>
                <NuxtLink
                  to="/jobs"
                  @click="isOpen = false"
                  class="my-4 inline-block"
                  >Jobs</NuxtLink
                >
              </li>
            </ul>
          </aside>
        </div>
      </nav>
    </header>
    <!-- output the page content -->
    <div class="container mx-auto p-4">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isOpen: false,
    };
  },
  methods: {
    drawer() {
      this.isOpen = !this.isOpen;
    },
  },
  watch: {
    isOpen: {
      immediate: true,
      handler(isOpen) {
        if (process.client) {
          if (isOpen) document.body.style.setProperty('overflow', 'hidden');
          else document.body.style.removeProperty('overflow');
        }
      },
    },
  },
  mounted() {
    document.addEventListener('keydown', (e) => {
      if (e.keyCode == 27 && this.isOpen) this.isOpen = false;
    });
  },
};
</script>

<style scoped>
/* .router-link-exact-active {
  color: black;
} */
.container {
  max-width: 1024px;
}
</style>
