<script setup>
import HomeView from '@/views/HomeView.vue'
import VideoView from '@/views/VideoView.vue'
import MainHeader from '@/components/MainHeader.vue'

const videos = [
  {
    id: 1,
    url: 'https://www.youtube.com/embed/TlWYgGyNnJo',
    thumbnail: 'https://img.youtube.com/vi/TlWYgGyNnJo/hqdefault.jpg'
  },
  {
    id: 2,
    url: 'https://www.youtube.com/embed/TlWYgGyNnJo',
    thumbnail: 'https://img.youtube.com/vi/TlWYgGyNnJo/hqdefault.jpg'
  }
]

// full page scroll
import fullpage from 'fullpage.js'
import 'fullpage.js/dist/fullpage.css'
import { onMounted } from 'vue'

onMounted(() => {
  new fullpage('#fullpage', {
    loopBottom: true,
    autoScrolling: true,
    scrollHorizontally: true
  })
})
</script>

<template>
  <main-header />
  <main class="full-pages" id="fullpage">
    <div class="full-page section">
      <HomeView />
    </div>
    <div v-for="video in videos" :key="video.id" class="full-page section">
      <VideoView v-bind="{ ...video }" />
    </div>
  </main>
</template>

<style lang="scss">
.full-page {
  height: 100vh;
  background-color: $color-background;
  padding: 30px;
}

.fp-watermark {
  display: none;
}

body:not(.fp-viewing-0) {
  #main-header {
    display: none;
  }
}
</style>
