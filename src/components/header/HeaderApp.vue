<template>
  <header class="sticky top-0 z-50 bg-white shadow-md">
    <nav class="container mx-auto px-4 py-3">
      <div class="flex justify-between items-center">
        <!-- Логотип и бургер меню -->
        <div class="flex items-center space-x-4">
          <!-- Бургер меню для мобилок (опционально) -->
          <button
            class="lg:hidden p-2 rounded-lg hover:bg-gray-100"
            @click="toggleMobileMenu"
          >
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"/>
            </svg>
          </button>

          <!-- Логотип -->
          <router-link
            to="/"
            class="flex items-center space-x-2 cursor-pointer hover:opacity-80 transition-opacity duration-200"
          >
            <div class="flex items-center">
              <div class="w-8 h-8 bg-primary-500 rounded-lg flex items-center justify-center">
                <span class="text-white font-bold text-lg">i</span>
              </div>
              <h1 class="text-xl font-bold text-gray-900 ml-2">WTB</h1>
            </div>
            <span class="text-sm text-gray-600 hidden md:inline">want to buy</span>
          </router-link>
        </div>

        <!-- Десктопная навигация -->
        <div class="hidden lg:flex items-center space-x-3">
          <!-- Кнопка создания запроса -->
          <router-link
            to="/create-request"
            class="flex items-center px-4 py-2 bg-primary-500 text-white rounded-lg hover:bg-primary-600 transition-colors duration-200 cursor-pointer"
          >
            <span class="text-lg font-bold mr-2">+</span>
            Создать запрос
          </router-link>

          <!-- Если пользователь не авторизован -->
          <div class="flex items-center space-x-2">
            <router-link
              to="/login"
              class="px-4 py-2 border border-primary-500 text-primary-600 rounded-lg hover:bg-primary-50 transition-colors duration-200 cursor-pointer"
            >
              Войти
            </router-link>

            <router-link
              to="/register"
              class="px-4 py-2 bg-primary-500 text-white rounded-lg hover:bg-primary-600 transition-colors duration-200 cursor-pointer"
            >
              Регистрация
            </router-link>
          </div>
        </div>

        <!-- Мобильная навигация (только кнопки) -->
        <div class="flex lg:hidden items-center space-x-2">
          <router-link
            to="/create-request"
            class="w-10 h-10 flex items-center justify-center bg-primary-500 text-white rounded-lg hover:bg-primary-600 transition-colors duration-200 cursor-pointer"
            title="Создать запрос"
          >
            <span class="text-xl font-bold">+</span>
          </router-link>

          <div class="flex items-center space-x-1">
            <router-link
              to="/login"
              class="px-3 py-1.5 border border-primary-500 text-primary-600 rounded-lg hover:bg-primary-50 transition-colors duration-200 cursor-pointer text-sm"
            >
              Войти
            </router-link>

            <router-link
              to="/register"
              class="px-3 py-1.5 bg-primary-500 text-white rounded-lg hover:bg-primary-600 transition-colors duration-200 cursor-pointer text-sm"
            >
              Рег.
            </router-link>
          </div>
        </div>
      </div>

      <!-- Мобильное меню (раскрывающееся) - опционально -->
      <div v-if="mobileMenuOpen" class="lg:hidden mt-4 pb-4 border-t pt-4">
        <div class="flex flex-col space-y-3">
          <router-link
            to="/"
            class="px-4 py-2 hover:bg-gray-100 rounded-lg transition-colors"
            @click="mobileMenuOpen = false"
          >
            Главная
          </router-link>
          <router-link
            to="/requests"
            class="px-4 py-2 hover:bg-gray-100 rounded-lg transition-colors"
            @click="mobileMenuOpen = false"
          >
            Все запросы
          </router-link>
          <router-link
            to="/how-it-works"
            class="px-4 py-2 hover:bg-gray-100 rounded-lg transition-colors"
            @click="mobileMenuOpen = false"
          >
            Как это работает
          </router-link>
        </div>
      </div>
    </nav>
  </header>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const mobileMenuOpen = ref(false)

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}
</script>
