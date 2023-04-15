<template>
  <div>
    <div v-for="storyId in stories">
      <StoryCard :storyId="storyId" />
    </div>
  </div>
</template>

<script setup>
// fetch the feeds
const { data: stories } = await useFetch(
  'https://hacker-news.firebaseio.com/v0/jobstories.json?print=pretty'
);
//console.log(stories);
stories.value.length = 20; // delete this later only here for development to limit the number of stories
</script>

<style>
body {
  background-color: #fbf0ea;
}
</style>
