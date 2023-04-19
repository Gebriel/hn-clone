<template>
  <div class="container bg-white mx-auto p-4 mb-4 rounded-lg">
    <!-- <NuxtLoadingIndicator /> -->
    <div class="flex justify-between gap-2">
      <div class="flex flex-col gap-4 col-span-2">
        <div class="flex flex-col overflow-ellipsis">
          <div class="text-slate-500 text-sm" v-if="comment.by">
            <div class="flex">
              <div><Icon name="ic:baseline-person-outline" /></div>
              <div class="">{{ comment.by }}</div>
            </div>
          </div>
          <div class="flex flex-col">
            <div v-if="comment.text">
              <p class="font-normal" v-html="comment.text"></p>
            </div>
          </div>
          <div class="text-slate-500 mx-1 text-sm" v-if="comment.time">
            <div class="flex">
              <div><Icon name="ic:outline-access-time" /></div>
              <p class="flex ml-1 mt-0.5">
                {{ getTime(comment.time) }}
              </p>
            </div>
          </div>
        </div>

        <div class="" v-if="comment.kids">
          <div v-for="kidId in comment.kids">
            <Comment :kidId="kidId" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useTimeAgo } from '@vueuse/core';

const { kidId } = defineProps(['kidId']);
const { data: comment } = await useFetch(
  `https://hacker-news.firebaseio.com/v0/item/${kidId}.json?print=pretty`
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
