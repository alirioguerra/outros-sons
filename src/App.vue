<script setup>
import HomeView from '@/views/HomeView.vue'
import VideoView from '@/views/VideoView.vue'
import MainHeader from '@/components/MainHeader.vue'
import VideoModal from '@/components/VideoModal.vue'
import { onMounted, ref } from 'vue'
import fullpage from 'fullpage.js'
import 'fullpage.js/dist/fullpage.css'

let modal = ref(false)
let activeUrl = ref('')

const videos = [
  {
    id: 1,
    url: 'https://www.youtube.com/embed/TlWYgGyNnJo?autoplay=1',
    thumbnail: 'https://img.youtube.com/vi/TlWYgGyNnJo/hqdefault.jpg',
    title: 'Título Video 1',
    description:
      'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut et massa mi. Aliquam in hendrerit urna. Pellentesque sit amet sapien fringilla, mattis ligula consectetur, ultrices mauris. Maecenas vitae mattis tellus.'
  },
  {
    id: 2,
    url: 'https://www.youtube.com/embed/TlWYgGyNnJo?autoplay=1',
    thumbnail: 'https://img.youtube.com/vi/TlWYgGyNnJo/hqdefault.jpg',
    title: 'Título Video 2',
    description:
      'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut et massa mi. Aliquam in hendrerit urna. Pellentesque sit amet sapien fringilla, mattis ligula consectetur, ultrices mauris. Maecenas vitae mattis tellus.'
  }
]

function toggleModal(url) {
  activeUrl.value = url
  modal.value = !modal.value
}

onMounted(() => {
  new fullpage('#fullpage', {
    loopBottom: true,
    autoScrolling: true,
    scrollHorizontally: true,
    navigation: true
  })
})
</script>

<template>
  <main-header :url="activeUrl" />
  <main class="full-pages" id="fullpage">
    <div class="full-page section">
      <HomeView />
    </div>
    <div v-for="video in videos" :key="video.id" class="full-page section">
      <VideoView @open-modal="toggleModal(video.url)" v-bind="{ ...video }" />
    </div>
  </main>
  <video-modal @close="toggleModal(null)" :active="modal" :url="activeUrl" />
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

#fp-nav.fp-right {
  right: 0;
}
#fp-nav ul li a span,
.fp-slidesNav ul li a span {
  background-color: $color-darken-orange;
}
</style>
