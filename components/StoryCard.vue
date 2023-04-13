<template>
  <div class="container bg-white mx-auto p-4 mb-4 rounded-lg">
    <div class="flex justify-between gap-2">
      <div class="flex flex-col gap-4 col-span-2">
        <div class="flex overflow-ellipsis">
          <div class="flex flex-col">
            <div>
              <a class="font-semibold" :href="story.url">{{ story.title }}</a>
            </div>
            <div class="md:hidden">
              <div class="flex text-slate-500">
                <a :href="story.url" target="_blank">{{
                  getHostName(story.url)
                }}</a>
                <a :href="story.url" target="_blank"
                  ><Icon name="ic:outline-launch"
                /></a>
              </div>
            </div>
          </div>
          <div class="text-slate-500 mx-1 text-sm">
            <div class="flex">
              (
              <div><Icon name="ic:baseline-person-outline" /></div>
              <div class="flex ml-1 mt-0.5">{{ story.by }}</div>
              )
            </div>
          </div>
        </div>

        <div class="flex justify-start gap-4">
          <div class="text-slate-500 text-sm">
            <div class="flex">
              <div><Icon name="mdi:medal-outline" /></div>
              <div class="flex ml-1 mt-0.5">
                {{ story.score }}
                <!-- <div class="hidden md:block ml-1">points</div> -->
              </div>
            </div>
          </div>
          <!-- <div class="text-slate-500 mx-1 text-sm">
            <div class="flex">
              <div><Icon name="ic:baseline-person-outline" /></div>
              <div class="flex ml-1 mt-0.5">{{ story.by }}</div>
            </div>
          </div> -->
          <div class="text-slate-500 mx-1 text-sm">
            <div class="flex">
              <div><Icon name="ic:outline-mode-comment" /></div>
              <div class="flex ml-1 mt-0.5">
                {{ story.descendants }}
                <!-- <div class="hidden md:block ml-1">comments</div> -->
              </div>
            </div>
          </div>
          <div class="text-slate-500 mx-1 text-sm">
            <div class="flex">
              <div><Icon name="ic:outline-access-time" /></div>
              <!-- <div class="flex ml-1 mt-0.5">{{ story.time }}</div> -->
              <p class="flex ml-1 mt-0.5">2 days</p>
            </div>
          </div>
        </div>
      </div>

      <div class="hidden md:block">
        <div class="flex text-slate-500">
          <a :href="story.url" target="_blank">{{ getHostName(story.url) }}</a>
          <a :href="story.url" target="_blank"
            ><Icon name="ic:outline-launch"
          /></a>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const { storyId } = defineProps(['storyId']);
const { data: story } = await useFetch(
  `https://hacker-news.firebaseio.com/v0/item/${storyId}.json?print=pretty`
);
const getHostName = (url) => {
  let domain = new URL(url);
  domain = domain.hostname;
  return domain;
};
</script>

<style scoped></style>
