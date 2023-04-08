<template>
  <div class="container shadow-sm bg-white mx-auto p-4 mb-4">
    <p>{{ story }}</p>
  </div>
</template>

<script setup>
const { storyId } = defineProps(['storyId']);
const { data: story } = await useFetch(
  `https://hacker-news.firebaseio.com/v0/item/${storyId}.json?print=pretty`
);
</script>

<style scoped></style>
