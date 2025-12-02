<template>
  <router-link
    :to="`/request/${request.id || 1}`"
    class="block bg-white rounded-xl shadow-md p-6 hover:shadow-lg transition-shadow duration-300 cursor-pointer"
  >
    <!-- Категория с цветным фоном -->
    <div class="mb-4">
      <span
        :class="getCategoryClass(request.category)"
        class="inline-flex items-center px-3 py-1 rounded-full text-sm font-medium"
      >
        {{ getCategoryIcon(request.category) }}
        {{ getCategoryLabel(request.category) }}
      </span>
    </div>

    <div class="flex justify-between items-start mb-4">
      <div class="flex-1">
        <div class="flex justify-between items-start">
          <h3 class="text-xl font-semibold text-gray-900">{{ request.title }}</h3>
          <span class="text-2xl font-bold text-green-600 ml-4">{{ formatPrice(request.price) }}</span>
        </div>
        <p class="text-gray-600 mt-2 line-clamp-2">{{ request.description }}</p>

        <div class="mt-4 flex items-center space-x-4 text-sm text-gray-500">
          <span class="flex items-center">
            <svg class="w-4 h-4 mr-1" fill="currentColor" viewBox="0 0 20 20">
              <path fill-rule="evenodd" d="M5.05 4.05a7 7 0 119.9 9.9L10 18.9l-4.95-4.95a7 7 0 010-9.9zM10 11a2 2 0 100-4 2 2 0 000 4z" clip-rule="evenodd" />
            </svg>
            {{ request.location }}
          </span>
          <span class="flex items-center">
            <svg class="w-4 h-4 mr-1" fill="currentColor" viewBox="0 0 20 20">
              <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-12a1 1 0 10-2 0v4a1 1 0 00.293.707l2.828 2.829a1 1 0 101.415-1.415L11 9.586V6z" clip-rule="evenodd" />
            </svg>
            {{ request.date }}
          </span>
        </div>
      </div>
    </div>

    <div class="flex justify-between items-center mt-4 pt-4 border-t">
      <div class="flex items-center">
        <div class="w-8 h-8 bg-gray-300 rounded-full flex items-center justify-center text-sm font-medium">
          {{ request.userInitials || 'П' }}
        </div>
        <span class="ml-2 text-sm text-gray-600">{{ request.userName || 'Покупатель' }}</span>
      </div>
      <span class="text-sm text-blue-600 font-medium">
        {{ request.offersCount || 0 }} предложений
      </span>
    </div>
  </router-link>
</template>

<script setup lang="ts">
import { computed } from 'vue'

// Определяем тип для запроса
interface RequestItem {
  id?: number
  title: string
  description: string
  price: number
  location: string
  date: string
  userName?: string
  userInitials?: string
  offersCount?: number
  category: string // Добавляем категорию
}

const props = defineProps<{
  request: RequestItem
}>()

// Функция для форматирования цены
const formatPrice = (price: number) => {
  return new Intl.NumberFormat('ru-RU').format(price) + ' ₽'
}

// Типы категорий и их стили
type CategoryType = 'electronics' | 'clothes' | 'realty' | 'services' | 'vehicles' | 'hobbies' | 'other'

// Маппинг категорий на русские названия
const categoryLabels: Record<CategoryType, string> = {
  electronics: 'Электроника',
  clothes: 'Одежда и обувь',
  realty: 'Недвижимость',
  services: 'Услуги',
  vehicles: 'Транспорт',
  hobbies: 'Хобби и отдых',
  other: 'Другое'
}

// Стили для каждой категории (background, text color)
const categoryStyles: Record<CategoryType, { bg: string, text: string, icon: string }> = {
  electronics: {
    bg: 'bg-blue-100',
    text: 'text-blue-800',
    icon: '📱'
  },
  clothes: {
    bg: 'bg-pink-100',
    text: 'text-pink-800',
    icon: '👕'
  },
  realty: {
    bg: 'bg-purple-100',
    text: 'text-purple-800',
    icon: '🏠'
  },
  services: {
    bg: 'bg-green-100',
    text: 'text-green-800',
    icon: '🔧'
  },
  vehicles: {
    bg: 'bg-yellow-100',
    text: 'text-yellow-800',
    icon: '🚗'
  },
  hobbies: {
    bg: 'bg-indigo-100',
    text: 'text-indigo-800',
    icon: '🎮'
  },
  other: {
    bg: 'bg-gray-100',
    text: 'text-gray-800',
    icon: '📦'
  }
}

// Функция для получения класса категории
const getCategoryClass = (category: string) => {
  const categoryKey = category.toLowerCase() as CategoryType
  const style = categoryStyles[categoryKey] || categoryStyles.other
  return `${style.bg} ${style.text}`
}

// Функция для получения иконки категории
const getCategoryIcon = (category: string) => {
  const categoryKey = category.toLowerCase() as CategoryType
  return categoryStyles[categoryKey]?.icon || categoryStyles.other.icon
}

// Функция для получения названия категории
const getCategoryLabel = (category: string) => {
  const categoryKey = category.toLowerCase() as CategoryType
  return categoryLabels[categoryKey] || categoryLabels.other
}
</script>

<style scoped>
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>
