<template>
  <div>
    <div v-for="storyId in stories">
      <StoryCard :storyId="storyId" />
    </div>
  </div>
</template>

<script setup>
//const stories = ref([]);

// fetch the feeds
const { data: stories } = await useFetch(
  'https://hacker-news.firebaseio.com/v0/showstories.json?print=pretty'
);
//console.log(stories);
stories.value.length = 20; // delete this later only here for development to limit the number of stories

// Promise.all(
//   feeds.value.map((e) =>
//     useFetch(
//       `https://hacker-news.firebaseio.com/v0/item/${e}.json?print=pretty`,
//       { key: e.toString() }
//     )
//   )
// ).then((responses) =>
//   responses.forEach((r) => stories.value.push(r.data.value))
// );
</script>

<style>
body {
  background-color: #fbf0ea;
}
</style>
