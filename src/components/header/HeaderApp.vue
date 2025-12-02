<template>
  <header class="sticky top-0 z-50 bg-white shadow-md">
    <div class="container mx-auto px-4 py-3">
      <div class="flex justify-between items-center">
        <!-- Логотип как ссылка -->
        <router-link
          to="/"
          class="flex items-center space-x-2 cursor-pointer hover:opacity-80 transition-opacity"
        >
          <h1 class="text-2xl font-bold text-blue-600">IWTB</h1>
          <span class="text-sm text-gray-600">i want to buy</span>
        </router-link>

        <nav class="flex items-center space-x-4">
          <!-- Кнопка создания запроса -->
          <router-link
            to="/request/new"
            class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors cursor-pointer"
          >
            + Создать запрос
          </router-link>

          <!-- Если пользователь не авторизован -->
          <router-link
            to="/login"
            class="px-4 py-2 border border-blue-600 text-blue-600 rounded-lg hover:bg-blue-50 transition-colors cursor-pointer"
          >
            Войти
          </router-link>

          <router-link
            to="/register"
            class="px-4 py-2 bg-green-600 text-white rounded-lg hover:bg-green-700 transition-colors cursor-pointer"
          >
            Регистрация
          </router-link>

          <!-- Если пользователь авторизован (будет позже) -->
          <!-- <div class="flex items-center space-x-2 cursor-pointer">
            <span>Имя пользователя</span>
            <div class="w-8 h-8 bg-gray-300 rounded-full"></div>
          </div> -->
        </nav>
      </div>
    </div>
  </header>
</template>

<script setup lang='ts'>
import { ref } from 'vue';

</script>

<style scoped>

</style>
