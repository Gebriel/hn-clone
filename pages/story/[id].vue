<template>
  <div>
    <div>
      <StoryDetail :story="story" />
    </div>
  </div>
</template>

<script setup>
const { id } = useRoute().params;
const uri = `https://hacker-news.firebaseio.com/v0/item/${id}.json?print=pretty`;
const { data: story } = await useFetch(uri, { key: id });
</script>

<style>
body {
  background-color: #fbf0ea;
}
</style>
