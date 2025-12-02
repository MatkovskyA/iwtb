<template>
  <div class="bg-gray-50">
    <div class="container mx-auto px-4 py-12">
      <div class="max-w-md mx-auto">
        <!-- Заголовок -->
        <div class="text-center mb-10">
          <h1 class="text-3xl font-bold text-gray-900">Вход в аккаунт</h1>
          <p class="mt-2 text-gray-600">
            Войдите чтобы продолжить
          </p>
        </div>

        <!-- Форма -->
        <div class="bg-white rounded-xl shadow-sm p-8">
          <form @submit.prevent="handleLogin" class="space-y-6">
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">
                Email
              </label>
              <input
                v-model="form.email"
                type="email"
                required
                placeholder="your@email.com"
                class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition"
              />
            </div>

            <div>
              <label class="block text-sm font-medium text-gray-700 mb-2">
                Пароль
              </label>
              <input
                v-model="form.password"
                type="password"
                required
                placeholder="Ваш пароль"
                class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition"
              />
            </div>

            <div class="flex items-center justify-between">
              <div class="flex items-center">
                <input
                  v-model="form.rememberMe"
                  type="checkbox"
                  class="mr-2 h-4 w-4 text-blue-600 focus:ring-blue-500 border-gray-300 rounded cursor-pointer"
                />
                <label class="text-sm text-gray-600 cursor-pointer">
                  Запомнить меня
                </label>
              </div>
              <a href="#" class="text-sm text-blue-600 hover:text-blue-500">
                Забыли пароль?
              </a>
            </div>

            <button
              type="submit"
              class="w-full py-3 bg-blue-600 text-white font-medium rounded-lg hover:bg-blue-700 transition-colors cursor-pointer"
            >
              Войти
            </button>

            <div class="text-center pt-4 border-t">
              <p class="text-gray-600">
                Нет аккаунта?
                <router-link to="/register" class="text-blue-600 font-medium hover:text-blue-500 ml-1">
                  Зарегистрироваться
                </router-link>
              </p>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const form = ref({
  email: '',
  password: '',
  rememberMe: false
})

const handleLogin = async () => {
  console.log('Вход:', form.value)
  router.push('/')
}
</script>
