<template>
  <div>
    <div>
      <div class="shadow-sm bg-white" v-for="story in stories">
        <div class="container mx-auto p-4 m-4">{{ story.title }}</div>
      </div>
    </div>
  </div>
</template>

<script setup>
// fetch the products
const { data } = await useFetch(
  'https://hacker-news.firebaseio.com/v0/topstories.json?print=pretty'
);
let stories = [];
data.value.forEach(async (storyId) => {
  const { data: story } = await useFetch(
    `https://hacker-news.firebaseio.com/v0/item/${storyId}.json?print=pretty`
  );
  stories.push(story.value);
});
console.log(stories);
</script>

<style lang="scss" scoped></style>
