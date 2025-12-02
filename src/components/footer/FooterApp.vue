<template>
  <footer class="bg-gray-900 text-white py-12 mt-auto">
    <div class="container mx-auto px-4">
      <div class="flex flex-col md:flex-row justify-between items-center">
        <div class="mb-8 md:mb-0">
          <div class="flex items-center space-x-3 mb-4">
            <div class="h-10 w-10 bg-primary-500 rounded-xl flex items-center justify-center">
              <span class="text-white font-bold text-xl">I</span>
            </div>
            <span class="text-2xl font-bold">IWTB</span>
          </div>
          <p class="text-gray-400">© 2024 IWTB. Все права защищены.</p>
        </div>
        <div class="text-center md:text-right">
          <p class="text-gray-400 mb-2">iwtb.ru — Покупай по своей цене!</p>
          <p class="text-gray-400">
            Свяжитесь с нами:
            <a href="mailto:hello@iwtb.ru" class="text-primary-400 hover:text-primary-300"
              >hello@iwtb.ru</a
            >
          </p>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { ref } from 'vue'
</script>

<style scoped lang=""></style>
