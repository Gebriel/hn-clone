<template>
  <div>
    <div>
      <StoryDetail :story="story" />
    </div>
    <div v-for="kidId in story.kids">
      <Comment :kidId="kidId" />
    </div>
  </div>
</template>

<script setup>
const { id } = useRoute().params;
const uri = `https://hacker-news.firebaseio.com/v0/item/${id}.json?print=pretty`;
const { data: story } = await useFetch(uri, { key: id });
// const noOfComments = story.value.descendants;
// console.log(noOfComments);
</script>

<style>
body {
  background-color: #fbf0ea;
}
</style>
