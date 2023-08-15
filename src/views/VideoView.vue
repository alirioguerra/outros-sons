<script setup>
const props = defineProps({
  url: String,
  id: Number,
  thumbnail: String,
  title: String,
  description: String
})

defineEmits(['openModal'])
</script>

<template>
  <div class="video-container">
    <div class="text-content">
      <h2>{{ props.title }}</h2>
      <p>{{ props.description }}</p>
    </div>
    <div class="video-wrapper">
      <a @click.prevent="$emit('openModal')" class="play-button" href="#">
        <img src="@/assets/icons/play-button.svg" alt="play" />
      </a>
      <img class="cover" :src="props.thumbnail" alt="video thumbnail" />
    </div>
  </div>
</template>

<style scoped lang="scss">
.video-container {
  position: relative;
  overflow: hidden;
  width: 100%;
  height: 100%;

  .video-wrapper {
    position: relative;

    &::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;

      background-color: #282727;
      opacity: 0.7;
      z-index: 1;
    }

    .play-button {
      position: absolute;
      top: 50%;
      right: 50%;
      transform: translate3d(50%, -50%, 0);
      z-index: 2;
      transition: all 0.3s ease-in-out;

      // hover light shadow effect
      &:hover {
        filter: drop-shadow(0 0 5px rgba(255, 255, 255, 0.5));
      }

      @media screen and (max-width: 768px) {
        width: rem-calc(70);
        height: rem-calc(70);
      }
    }
    .cover {
      aspect-ratio: 16/9;
      width: 100%;
      object-fit: cover;
    }
  }

  .text-content {
    position: absolute;
    bottom: 50%;
    right: 0;
    padding: 30px;
    transform: translateY(50%);
    z-index: 2;
    max-width: rem-calc(550);

    @media only screen and (max-width: 768px) {
      display: none;
    }

    h2 {
      opacity: 0;
      transform: translate3d(0, 50px, 0);
      font-size: rem-calc(50);
      font-weight: 700;
      color: $color-orange;
      margin-bottom: rem-calc(70);
    }

    p {
      opacity: 0;
      transform: translate3d(0, 50px, 0);
      font-size: rem-calc(18);
      line-height: rem-calc(28);
      font-weight: 400;
      color: $color-background;
    }
  }
}

.active {
  .text-content {
    h2 {
      opacity: 1;
      transform: translate3d(0, 0, 0);
      transition: all 0.3s ease-in-out 0.3s;
    }

    p {
      opacity: 1;
      transform: translate3d(0, 0, 0);
      transition: all 0.3s ease-in-out 0.5s;
    }
  }
}
</style>
