<template>
  <header class="sticky top-0 z-50 bg-white shadow-md">
    <nav class="container mx-auto px-4 py-3">
      <div class="flex justify-between items-center">
        <!-- Логотип и бургер меню -->
        <div class="flex items-center space-x-4">
          <!-- Бургер меню для мобилок -->
          <button
            class="lg:hidden p-2 rounded-lg hover:bg-gray-100"
            @click="toggleMobileMenu"
          >
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                :d="mobileMenuOpen ? 'M6 18L18 6M6 6l12 12' : 'M4 6h16M4 12h16M4 18h16'"
              />
            </svg>
          </button>

          <!-- Логотип -->
          <router-link
            to="/"
            class="flex items-center space-x-2 cursor-pointer hover:opacity-80 transition-opacity duration-200"
            @click="closeMobileMenu"
          >
            <div class="flex items-center">
              <h1 class="text-xl font-bold text-blue-900 ml-2">IWTB</h1>
            </div>
            <span class="text-sm text-gray-600 hidden md:inline">I want to buy</span>
          </router-link>
        </div>

        <!-- Десктопная навигация -->
        <div class="hidden lg:flex items-center space-x-3">
          <!-- Кнопка создания запроса -->
          <router-link
            to="/create-request"
            class="flex items-center px-4 py-2 bg-primary-500 text-black border rounded-lg hover:bg-primary-600 transition-colors duration-200 cursor-pointer"
          >
            <span class="text-lg font-bold mr-2">+</span>
            Создать запрос
          </router-link>

          <!-- Если пользователь не авторизован -->
          <div class="flex items-center space-x-2">
            <router-link
              to="/login"
              class="px-4 py-2 bg-green-600 text-white rounded-lg hover:bg-green-700 transition-colors duration-200 cursor-pointer"
            >
              Войти
            </router-link>

            <router-link
              to="/register"
              class="px-4 py-2 bg-blue-600 text-white font-medium rounded-lg hover:bg-blue-700 transition-colors cursor-pointer"
            >
              Регистрация
            </router-link>
          </div>
        </div>

        <!-- Мобильная навигация (только кнопки) -->
        <div class="flex lg:hidden items-center space-x-2">
          <router-link
            to="/create-request"
            class="w-10 h-10 flex items-center justify-center border bg-primary-500 text-black rounded-lg hover:bg-gray-100 transition-colors duration-200 cursor-pointer"
            title="Создать запрос"
            @click="closeMobileMenu"
          >
            <span class="text-xl font-bold">+</span>
          </router-link>

          <div class="flex items-center space-x-1">
            <router-link
              to="/login"
              class="px-3 py-1.5 bg-green-600 text-white rounded-lg hover:bg-green-700 transition-colors duration-200 cursor-pointer text-sm"
              @click="closeMobileMenu"
            >
              Войти
            </router-link>

            <router-link
              to="/register"
              class="px-3 py-1.5 bg-blue-600 text-white font-medium rounded-lg hover:bg-blue-700 transition-colors cursor-pointer text-sm"
              @click="closeMobileMenu"
            >
              Рег.
            </router-link>
          </div>
        </div>
      </div>

      <!-- Мобильное меню (раскрывающееся) -->
      <div
        v-if="mobileMenuOpen"
        class="lg:hidden mt-4 pb-4 border-t pt-4 transition-all duration-300 ease-in-out"
        :class="{ 'opacity-100 translate-y-0': mobileMenuOpen, 'opacity-0 -translate-y-4': !mobileMenuOpen }"
      >
        <div class="flex flex-col space-y-3">
          <router-link
            to="/"
            class="px-4 py-2 hover:bg-gray-100 rounded-lg transition-colors"
            @click="closeMobileMenu"
          >
            Главная
          </router-link>
          <router-link
            to="/requests"
            class="px-4 py-2 hover:bg-gray-100 rounded-lg transition-colors"
            @click="closeMobileMenu"
          >
            Все запросы
          </router-link>
          <router-link
            to="/how-it-works"
            class="px-4 py-2 hover:bg-gray-100 rounded-lg transition-colors"
            @click="closeMobileMenu"
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

const closeMobileMenu = () => {
  mobileMenuOpen.value = false
}

// Закрываем меню при клике вне его (опционально)
const closeOnClickOutside = (event: MouseEvent) => {
  const target = event.target as HTMLElement
  if (!target.closest('header')) {
    closeMobileMenu()
  }
}

// Добавляем обработчик клика вне меню
if (typeof window !== 'undefined') {
  document.addEventListener('click', closeOnClickOutside)
}
</script>
