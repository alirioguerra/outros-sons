<script setup>
const props = defineProps({
  url: String,
  id: Number,
  thumbnail: String
})
</script>

<template>
  <div class="video-container">
    <div class="video-wrapper">
      <a class="play-button" href="#">
        <img src="@/assets/icons/play-button.svg" alt="play" />
      </a>
      <img class="cover" :src="props.thumbnail" alt="video thumbnail" />
    </div>
    <!-- <iframe width="560" height="315" :src="props.url" frameborder="0" allowfullscreen /> -->
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

    .play-button {
      position: absolute;
      top: 50%;
      right: 30%;
      transform: translate3d(-50%, -50%, 0);
    }
    .cover {
      aspect-ratio: 16/9;
      width: 100%;
      object-fit: cover;
    }
  }
}
</style>
