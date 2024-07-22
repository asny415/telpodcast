<script setup lang="ts">
import { onMounted, ref } from 'vue'
const tutarials = ref([])
const contact = ref('')
const hots = ref([])
const hotsTitle = ref('')
onMounted(async () => {
  const lang = navigator.language
  const rsp = await fetch(`/hots.json`)
  const globalhots = await rsp.json()
  hots.value = globalhots[lang.slice(0, 2)] || globalhots['zh'] || []
  contact.value = lang == 'zh-CN' ? '<a href="mailto:asny415@gmail.com">联系我</a>' : '<a href="mailto:asny415@gmail.com">Contact me</a>'
  hotsTitle.value = lang == 'zh-CN' ? '热门排行' : 'Hots'
  tutarials.value = lang == 'zh-CN' ? [
    '一、添加机器人 <a href="https://t.me/telpodcast_bot">TelPodcast</a>',
    "二、直接给机器人发送播客名字进行搜索",
    "三、订阅你感兴趣的播客，有新单集发布时你将直接收到音频通知"

  ] : [
    "step1: add bot telpodcast to your contact!",
    "step2: Send the name of your favorite podcast to the bot.",
    "step3: Subscribe to it, and you will receive notifications when the podcast is updated."
  ]
})
</script>

<template>
  <div class="root">
    <div class="header">
      <img class="logo" src="/telpodcast.jpg" />
      <div class="titles">
        <span class="title">Telpodcast</span>
        <span class="subtitle">Listen podcast from telegram</span>
      </div>
    </div>
    <div class="tutarial">
      <div v-for="line in tutarials" class="tutaline" v-html="line"></div>
    </div>
    <div class="hots">
      <div class="title">{{ hotsTitle }}</div>
      <div>
        <div class="hotline" v-for="hot in hots">
          <img style="width:2.5em;height: 2.5em;" :src="hot.thumb" />
          <a style="margin-left: 1em; width:8em; text-align: center;text-overflow: ellipsis;overflow: hidden;white-space: nowrap;"
            :href="hot.home" target="_blank">{{ hot.name }}</a>
          <span style="flex:1;margin-left:1em;text-overflow: ellipsis;overflow: hidden;white-space: nowrap;">{{
        hot.slogan }}</span>
        </div>
      </div>
    </div>
    <div class="footer">
      <div style="display: flex;align-items: center;">Powered by asny415 && Deno<img
          style="margin-left: 1em; width:1em;height:1em;" src="/vite-deno.svg" /></div>
      <div v-html="contact"></div>
    </div>
  </div>
</template>

<style scoped>
.titles {
  display: flex;
  flex-direction: column;
  align-items: start;
}

.title {
  font-size: x-large;
  text-align: center;
  margin-bottom: 2em;
}

.hotline {
  margin-top: 0.3em;
  display: flex;
  align-items: center;
  justify-content: stretch;
  margin-bottom: 0.5em;
}

.hots {
  flex: 1;
  width: 90vw;
  max-width: 50em;
  padding: 1em;
  margin-top: 3em;
}

.footer {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-family: 'Courier New', Courier, monospace;
  opacity: 0.6;
  padding: 1em 0 1em 0;
  font-size: small;
  font-weight: bold;
  margin-top: 10em;
}

.tutaline {
  font-family: fantasy;
  margin-bottom: 0.5em;
}

.tutarial {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  width: 90vw;
  max-width: 20em;
  padding: 1em;
  margin-top: 3em;
}

.logo {
  width: 5em;
  height: 5em;
  border-radius: 2.5em;
  box-shadow: 0 1px 2px 0 rgb(0 0 0 / 0.05);
  margin-right: 1em;
}

.header {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  padding-top: 2em;
}

.title {
  font-size: x-large;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}
</style>
