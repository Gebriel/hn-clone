<template>
  <div class="container bg-white mx-auto p-4 mb-4 rounded-lg">
    <NuxtLoadingIndicator />
    <div class="flex justify-between gap-2">
      <div class="flex flex-col gap-4 col-span-2">
        <div class="flex overflow-ellipsis">
          <div class="flex flex-col">
            <div>
              <NuxtLink :to="`/story/${story.id}`" class="flex">
                <p class="font-semibold">{{ story.title }}</p>
              </NuxtLink>
            </div>
            <div class="md:hidden" v-if="story.url">
              <div class="flex text-slate-500">
                <a :href="story.url" target="_blank"
                  ><p>{{ getHostName(story.url) }}</p></a
                >
                <a :href="story.url" target="_blank"
                  ><Icon name="ic:outline-launch"
                /></a>
              </div>
            </div>
          </div>
          <div class="text-slate-500 mx-1 text-sm" v-if="story.by">
            <div class="flex">
              (
              <div><Icon name="ic:baseline-person-outline" /></div>
              <div class="flex ml-1 mt-0.5">{{ story.by }}</div>
              )
            </div>
          </div>
        </div>

        <div class="flex justify-start gap-4" v-if="story.score">
          <div class="text-slate-500 text-sm">
            <div class="flex">
              <div><Icon name="mdi:medal-outline" /></div>
              <div class="flex ml-1 mt-0.5">
                {{ story.score }}
              </div>
            </div>
          </div>

          <div class="text-slate-500 mx-1 text-sm" v-if="story.descendants">
            <div class="flex">
              <NuxtLink :to="`/story/${story.id}`" class="flex">
                <div><Icon name="ic:outline-mode-comment" /></div>
                <div class="flex ml-1 mt-0.5">
                  <p class="">{{ story.descendants }}</p>
                </div>
              </NuxtLink>
            </div>
          </div>
          <div class="text-slate-500 mx-1 text-sm" v-if="story.time">
            <div class="flex">
              <div><Icon name="ic:outline-access-time" /></div>
              <p class="flex ml-1 mt-0.5">
                {{ getTime(story.time).value }}
              </p>
            </div>
          </div>
        </div>
      </div>

      <div class="hidden md:block" v-if="story.url">
        <div class="flex text-slate-500">
          <a :href="story.url" target="_blank"
            ><p>{{ getHostName(story.url) }}</p></a
          >
          <a :href="story.url" target="_blank"
            ><Icon name="ic:outline-launch"
          /></a>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useTimeAgo } from '@vueuse/core';

const { storyId } = defineProps(['storyId']);
const { data: story } = await useFetch(
  `https://hacker-news.firebaseio.com/v0/item/${storyId}.json?print=pretty`
);

const getHostName = (url) => {
  try {
    //console.log(url);
    let domain = new URL(url);
    domain = domain.hostname;
    return domain;
  } catch (error) {
    console.log(error);
  }

  return 'invalid url';
};

const getTime = (time) => {
  const timeAgo = useTimeAgo(time * 1000);
  return timeAgo;
};
</script>

<style scoped></style>
