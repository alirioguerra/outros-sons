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
let activeRelatedLinks = ref([])
let videos = ref([])

fetch('/videos.json')
  .then((res) => res.json())
  .then((data) => (videos.value = data))

function toggleModal({ relatedLinks, url }) {
  activeUrl.value = url
  activeRelatedLinks.value = relatedLinks
  modal.value = !modal.value
  document.body.classList.toggle('no-scroll')
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
      <div class="desktop-text">
        <h2>{{ video.title }}</h2>
        <p v-html="video.description" />
      </div>
      <VideoView @open-modal="toggleModal(video)" v-bind="{ ...video }" />
    </div>
  </main>
  <video-modal
    v-if="modal"
    @close="toggleModal({ relatedLinks: [], url: '' })"
    :related-links="activeRelatedLinks"
    :active="modal"
    :url="activeUrl"
  />
</template>

<style lang="scss">
.fp-viewing-0 {
  .full-page {
    padding: 0 30px 30px 30px;
  }
}
.full-page {
  height: 100vh;
  background-color: $color-background;
  padding: 30px;

  @media only screen and (max-width: 768px) {
    padding: 15px;
    display: flex;
    align-items: center;
    flex-direction: column;
  }
}

.fp-watermark {
  display: none;
}

body:not(.fp-viewing-0) {
  #main-header {
    display: none;
  }

  @media only screen and (max-width: 768px) {
    .fp-overflow {
      display: grid;
      grid-template-columns: 1fr;
      grid-template-rows: 1fr 1fr;
    }
  }
}

#fp-nav.fp-right {
  right: 0;
}

#fp-nav ul li a span,
.fp-slidesNav ul li a span {
  background-color: $color-darken-orange;
}

.desktop-text {
  display: none;

  @media only screen and (max-width: 768px) {
    display: block;
    margin-bottom: rem-calc(30);

    h2 {
      font-size: rem-calc(42);
      font-weight: 700;
      color: $color-orange;
      margin-bottom: rem-calc(30);
    }

    p {
      max-width: rem-calc(550);
      font-size: rem-calc(14);
      line-height: rem-calc(18);
      font-weight: 400;
      color: $color-blue;

      a {
        color: $color-blue;
        text-decoration: underline;
        font-weight: bold;
      }
    }
  }
}
</style>
