<template>
  <div>
    <header class="w-full header">
      <nav class="mx-auto p-4 shadow">
        <div class="flex items-center justify-between">
          <!-- Header logo Desktop-->
          <div class="hidden md:block">
            <HackerNews />
          </div>
          <!-- Header logo Mobile-->
          <div class="md:hidden">
            <HackerNewsMobile />
          </div>

          <!-- Mobile toggle -->
          <div class="md:hidden">
            <button @click="drawer" class="pt-1.5">
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
                class="absolute top-0 right-0 mt-4 mr-4 pt-1"
                @click="isOpen = false"
              >
                <svg
                  class="w-8 h-8"
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
              class="flex w-full items-center pb-6 border-b"
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
a.router-link-active {
  color: #fbf0ea;
  background-color: black;
  padding: 5px;
  border-radius: 20%;
}
.container {
  max-width: 1024px;
}
.header {
  background-color: #ed702d;
}
</style>
