<script setup lang="ts">
  import HeaderApp from './components/header/HeaderApp.vue';
  import FooterApp from './components/footer/FooterApp.vue';
</script>

<template>
  <div class="flex flex-col min-h-screen">
    <HeaderApp />
    <main class="flex-grow">
      <router-view />
    </main>
    <FooterApp />
  </div>
</template>

<style scoped></style>
