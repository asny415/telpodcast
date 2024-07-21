<script setup lang="ts">
import { onMounted, ref } from 'vue'
const tutarials = ref([])
const contact = ref('')
onMounted(() => {
  const lang = navigator.language
  contact.value = lang == 'zh-CN' ? '<a href="mailto:asny415@gmail.com">联系我</a>' : '<a href="mailto:asny415@gmail.com">Contact me</a>'
  tutarials.value = lang == 'zh-CN' ? [
    '一、添加机器人 <a href="https://t.me/telpodcast_bot">TelPodcast</a>',
    "二、直接给机器人发送播客名字进行搜索",
    "三、订阅你找到的播客，有新单集发布时你将直接收到单集音频"

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
      <span class="title">Telpodcast</span>
    </div>
    <div class="tutarial">
      <div v-for="line in tutarials" class="tutaline" v-html="line"></div>
    </div>
    <div class="hots"></div>
    <div class="footer">
      <div>Powered by asny415</div>
      <div v-html="contact"></div>
    </div>
  </div>
</template>

<style scoped>
.hots {
  flex: 1;
}

.footer {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-family: 'Courier New', Courier, monospace;
  opacity: 0.6;
  padding: 2em 0 5em 0;
  font-size: small;
  font-weight: bold;
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
  width: 50vw;
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
