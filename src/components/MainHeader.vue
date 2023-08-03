<script setup></script>
<template>
  <header id="main-header">
    <img src="@/assets/logo.svg" alt="logo outros sons" />
  </header>
</template>

<style scoped lang="scss">
#main-header {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding: rem-calc(15 30 0 30);
  opacity: 1;
  transition: opacity 0.9s ease;

  img {
    max-width: rem-calc(100);
  }
}
</style>
