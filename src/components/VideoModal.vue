<script setup>
const props = defineProps({
  url: String,
  active: {
    type: Boolean,
    default: false
  },
  relatedLinks: {
    type: Array,
    default: () => []
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
    <ul class="related-links">
      <h2>Links úteis</h2>
      <li v-for="link in props.relatedLinks" :key="link.id">
        <a :href="link.url" target="_blank">
          {{ link.title }}
        </a>
      </li>
    </ul>
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
  background-color: rgba(0, 0, 0, 1);
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease-in-out;
  aspect-ratio: 16/9;

  display: grid;
  grid-template-columns: 1fr 300px;
  gap: rem-calc(60);

  @media (max-width: 768px) {
    grid-template-columns: 1fr;
    grid-template-rows: 200px 1fr;
    gap: 30px;
  }

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

.related-links {
  display: flex;
  flex-direction: column;
  gap: rem-calc(30);
  padding: 90px 0;
  list-style: none;
  margin: 0;
  overflow-y: auto;
  max-height: 100%;
  font-size: rem-calc(18);

  h2 {
    font-weight: 800;
    font-size: rem-calc(30);
    color: $color-darken-orange;
  }

  li {
    a {
      color: $color-background;
      text-decoration: underline;
      transition: all 0.3s ease-in-out;
      line-height: 1.4;

      &:hover {
        color: $color-darken-orange;
      }
    }
  }

  @media (max-width: 768px) {
    padding: 30px 0;
    gap: 15px;

    h2 {
      font-size: rem-calc(24);
    }

    li {
      a {
        font-size: rem-calc(14);
        line-height: 1.2;
      }
    }
  }
}
</style>
