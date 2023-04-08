<template>
  <div>
    <div class="shadow-sm bg-white" v-for="story in stories">
      <div class="container mx-auto p-4 mb-4">{{ story.title }}</div>
    </div>
  </div>
</template>

<script setup>
const stories = ref([]);

// fetch the feeds
const { data: feeds } = await useFetch(
  'https://hacker-news.firebaseio.com/v0/beststories.json?print=pretty'
);

feeds.value.length = 10;

Promise.all(
  feeds.value.map((e) =>
    useFetch(
      `https://hacker-news.firebaseio.com/v0/item/${e}.json?print=pretty`,
      { key: e.toString() }
    )
  )
).then((responses) =>
  responses.forEach((r) => stories.value.push(r.data.value))
);

// watchEffect(
//   feeds,
//   Promise.all(
//     feeds.value.map((e) =>
//       useFetch(
//         `https://hacker-news.firebaseio.com/v0/item/${e}.json?print=pretty`,
//         { key: e.toString() }
//       )
//     )
//   ).then((responses) =>
//     responses.forEach((r) => stories.value.push(r.data.value))
//   )
// );
</script>

<style lang="scss" scoped></style>
