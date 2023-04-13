<template>
  <div class="container bg-white mx-auto p-4 mb-4 rounded-lg flex">
    <div class="flex-auto w-64">
      <div class="flex flex-col gap-2">
        <div>{{ story.title }}</div>
        <div class="flex">
          <div class="text-slate-500">
            <div class="flex">
              <div><Icon name="mdi:medal-outline" /></div>
              <div class="ml-1 mt-0.5">{{ story.score }} points</div>
            </div>
          </div>
          <div class="text-slate-500 mx-5">
            <div class="flex">
              <div><Icon name="ic:baseline-person-outline" /></div>
              <div class="ml-1 mt-0.5">{{ story.by }}</div>
            </div>
          </div>
          <div class="text-slate-500 mx-5">
            <div class="flex">
              <div><Icon name="ic:outline-mode-comment" /></div>
              <div class="ml-1 mt-0.5">{{ story.descendants }} comments</div>
            </div>
          </div>
          <div class="text-slate-500 mx-5">
            <div class="flex">
              <div><Icon name="ic:outline-access-time" /></div>
              <div class="ml-1 mt-0.5">{{ story.time }}</div>
            </div>
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
