<template>
  <div class="container mx-auto px-4 py-8">
    <div class="max-w-4xl mx-auto">
      <div class="mb-6">
        <router-link
          to="/"
          class="text-blue-600 hover:text-blue-800 cursor-pointer flex items-center"
        >
          <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18" />
          </svg>
          Назад к запросам
        </router-link>
      </div>

      <div class="bg-white rounded-xl shadow-lg p-6 mb-6">
        <div class="flex justify-between items-start mb-4">
          <div>
            <h1 class="text-2xl font-bold text-gray-900 mb-2">iPhone 15 Pro 256GB</h1>
            <div class="flex items-center space-x-4 text-sm text-gray-600">
              <span class="flex items-center">
                <svg class="w-4 h-4 mr-1" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M5.05 4.05a7 7 0 119.9 9.9L10 18.9l-4.95-4.95a7 7 0 010-9.9zM10 11a2 2 0 100-4 2 2 0 000 4z" clip-rule="evenodd" />
                </svg>
                Казань
              </span>
              <span class="flex items-center">
                <svg class="w-4 h-4 mr-1" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-12a1 1 0 10-2 0v4a1 1 0 00.293.707l2.828 2.829a1 1 0 101.415-1.415L11 9.586V6z" clip-rule="evenodd" />
                </svg>
                Сегодня
              </span>
            </div>
          </div>
          <span class="text-3xl font-bold text-green-600">90 000 ₽</span>
        </div>

        <div class="mb-6">
          <h2 class="text-lg font-semibold mb-2">Описание запроса</h2>
          <p class="text-gray-700">
            Ищу новый или б/у iPhone 15 Pro в отличном состоянии.
            Цвет не важен, главное чтобы батарея была в хорошем состоянии.
          </p>
        </div>

        <div class="mb-6">
          <h2 class="text-lg font-semibold mb-4">Предложения продавцов</h2>
          <div class="space-y-4">
            <div class="border rounded-lg p-4">
              <div class="flex justify-between items-center">
                <div>
                  <h3 class="font-medium">Иван Петров</h3>
                  <p class="text-sm text-gray-600">iPhone 15 Pro, 256GB, Синий</p>
                </div>
                <div class="text-right">
                  <p class="text-lg font-bold text-gray-900">95 000 ₽</p>
                  <button class="mt-2 px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 cursor-pointer">
                    Связаться
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div>
          <h2 class="text-lg font-semibold mb-4">Оставить предложение</h2>
          <div class="border rounded-lg p-4">
            <textarea
              class="w-full border rounded-lg p-3 mb-3"
              rows="4"
              placeholder="Опишите ваше предложение..."
            ></textarea>
            <div class="flex justify-between items-center">
              <input
                type="number"
                class="border rounded-lg p-2 w-32"
                placeholder="Цена"
              />
              <button class="px-6 py-2 bg-green-600 text-white rounded-lg hover:bg-green-700 cursor-pointer">
                Отправить предложение
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useRoute } from 'vue-router'

const route = useRoute()
</script>
