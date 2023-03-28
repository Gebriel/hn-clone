<template>
  <div>
    <div class="grid grid-cols-4 gap-5">
      <div v-for="story in stories">
        <div>{{ story }}</div>
      </div>
    </div>
  </div>
</template>

<script setup>
// fetch the products
const { data: stories } = await useFetch(
  'https://hacker-news.firebaseio.com/v0/topstories.json?print=pretty'
);

console.log(stories.value);
</script>

<style lang="scss" scoped></style>
