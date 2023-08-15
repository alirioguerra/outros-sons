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
    id: 3,
    url: 'https://www.youtube.com/embed/N6b7i8oQC3g?autoplay=1&fullscreen=1',
    thumbnail: 'https://img.youtube.com/vi/N6b7i8oQC3g/hqdefault.jpg',
    title: 'Acessibilidade Surda - Cultura',
    description:
      'Neste episódio você vai conhecer as vivências da artista Cecília Lima e da estudante de cinema Beatriz Cruz nos espaços culturais de Brasília, elas expõem as dificuldades de acesso às obras e produtos artísticos para pessoas surdas e com deficiência auditiva. Ainda nesse bloco, Cecília Lima comenta sobre a exposição em conjunto com a artista e professora da Universidade de Brasília (UnB), Iracema Barbosa.'
  },
  {
    id: 3,
    url: 'https://www.youtube.com/embed/c0akPkne0EQ?autoplay=1&fullscreen=1',
    thumbnail: 'https://img.youtube.com/vi/c0akPkne0EQ/hqdefault.jpg',
    title: 'Acessibilidade Surda - Educação',
    description:
      'No episódio de Educação, a coordenadora da Escola Bilíngue de Taguatinga -DF, Adriana Gomes, expõe as dificuldades enfrentadas pelos surdos no processo de aprendizagem devido à falta de acessibilidade no ensino brasileiro. O episódio também apresenta a relação construída entre a professora ouvinte de artes da Escola Bilíngue de Taguatinga - DF, Rosa Pires, com o aluno surdo de altas habilidades em desenho, Kauan de Sousa.'
  },
  {
    id: 1,
    url: 'https://www.youtube.com/embed/sm3uUk8dCko?autoplay=1&fullscreen=1',
    thumbnail: 'https://img.youtube.com/vi/sm3uUk8dCko/hqdefault.jpg',
    title: 'Acessibilidade Surda - Esporte',
    description:
      'Neste episódio, a surdo atleta, duas vezes bronze no Campeonato Mundial de Handebol de Surdos e assessora de projetos da Federação Brasiliense Desportiva dos Surdos (FBDS), Déborah Dias, compartilha as suas experiências, expõe as carências públicas da área e opina sobre a importância social do esporte para os surdos e deficientes auditivos.'
  },
  {
    id: 2,
    url: 'https://www.youtube.com/embed/gKsfgCkd4OE?autoplay=1&fullscreen=1',
    thumbnail: 'https://img.youtube.com/vi/gKsfgCkd4OE/hqdefault.jpg',
    title: 'Acessibilidade surda - Saúde',
    description:
      'No episódio de saúde, a psicóloga Luma Gaudad explica a importância da inclusão e acessibilidade na saúde, principalmente na área da psicologia. Ainda neste bloco, o assistente de pesquisa clínica, Kenzo Watanabe, conta a sua experiência na área profissional e a importância da implementação da libras nas faculdades de saúde.'
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
      <div class="desktop-text">
        <h2>{{ video.title }}</h2>
        <p>{{ video.description }}</p>
        <a href="#">link útil</a>
      </div>
      <VideoView @open-modal="toggleModal(video.url)" v-bind="{ ...video }" />
    </div>
  </main>
  <video-modal v-if="modal" @close="toggleModal(null)" :active="modal" :url="activeUrl" />
</template>

<style lang="scss">
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
      line-height: rem-calc(14);
      font-weight: 400;
      color: $color-blue;
    }
  }
}
</style>
