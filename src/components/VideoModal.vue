<script setup>
const props = defineProps({
  url: String,
  active: {
    type: Boolean,
    default: false
  }
})

defineEmits(['close'])
</script>

<template>
  <div :class="['full-screen', { active: active }]">
    <a @click="$emit('close')" href="#" class="close">
      <img src="@/assets/icons/close-button.svg" alt="close" />
    </a>
    <iframe v-if="props.url" width="100%" height="100%" :src="props.url" allowfullscreen />
  </div>
</template>

<style scoped lang="scss">
.full-screen {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
  width: 100%;
  height: 100%;
  padding: rem-calc(30);
  background-color: rgba(0, 0, 0, 0.9);
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease-in-out;
  aspect-ratio: 16/9;

  .close {
    position: absolute;
    top: 0;
    right: 0;
    z-index: 2;
    transition: all 0.3s ease-in-out;

    &:hover {
      transform: scale(1.1);
    }
  }
  &.active {
    opacity: 1;
    visibility: visible;
  }
}
</style>
