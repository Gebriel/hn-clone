<template>
  <div class="container bg-white mx-auto p-4 mb-4 rounded-lg flex">
    <div class="flex-auto w-64">
      <div class="flex flex-col">
        <div>{{ story.title }}</div>
        <div class="flex">
          <div class="text-slate-500">
            <Icon name="mdi-light:trophy" />
            {{ story.score }} points
          </div>
          <div class="text-slate-500 mx-4">
            <Icon name="mdi-light:account" />
            {{ story.by }}
          </div>
          <div class="text-slate-500 mx-4">
            <Icon name="mdi-light:message-text" />{{ story.descendants }}
            comments
          </div>
          <div class="text-slate-500 mx-4">
            <Icon name="mdi-light:clock" />{{ story.time }}
          </div>
        </div>
      </div>
    </div>
    <div class="flex-auto w-32">
      <div>{{ story.url }}</div>
    </div>
  </div>
</template>

<script setup>
const { storyId } = defineProps(['storyId']);
const { data: story } = await useFetch(
  `https://hacker-news.firebaseio.com/v0/item/${storyId}.json?print=pretty`
);
</script>

<style scoped></style>
