<template>
  <div class="min-h-screen bg-gradient-to-b from-gray-50 to-white">
    <!-- Hero Section -->
    <section class="container mx-auto px-4 py-12 md:py-20">
      <div class="max-w-4xl mx-auto text-center">
        <h1 class="text-5xl md:text-7xl font-bold text-gray-900 mb-6 leading-tight">
          Твой маркет покупателя
        </h1>
        <p class="text-xl md:text-2xl text-gray-600 mb-10 max-w-3xl mx-auto leading-relaxed">
          Покупатели публикуют что хотят купить и сколько готовы заплатить.
          <br class="hidden md:block">
          Продавцы предлагают свои товары по запросу.
        </p>

        <div class="flex flex-col sm:flex-row gap-4 justify-center max-w-md mx-auto">
          <button
            @click="router.push('/register')"
            class="px-8 py-4 bg-primary-500 text-white text-lg font-semibold rounded-xl hover:bg-primary-600 transition-all shadow-lg hover:shadow-xl hover:-translate-y-0.5 cursor-pointer"
          >
            🛍️ Создать запрос
          </button>
          <a
            href="#requests"
            class="px-8 py-4 bg-white text-gray-800 text-lg font-semibold rounded-xl border-2 border-gray-200 hover:border-primary-400 hover:text-primary-600 transition-all shadow-md hover:shadow-lg cursor-pointer text-center"
          >
            🔍 Смотреть запросы
          </a>
        </div>
      </div>
    </section>

    <!-- Stats -->
    <div class="container mx-auto px-4 mb-12">
      <div class="grid grid-cols-2 md:grid-cols-4 gap-6 max-w-4xl mx-auto">
        <div class="bg-white p-6 rounded-2xl shadow-sm border text-center">
          <div class="text-3xl font-bold text-primary-500 mb-2">1,247</div>
          <div class="text-gray-600">Пользователей</div>
        </div>
        <div class="bg-white p-6 rounded-2xl shadow-sm border text-center">
          <div class="text-3xl font-bold text-primary-500 mb-2">3,568</div>
          <div class="text-gray-600">Запросов</div>
        </div>
        <div class="bg-white p-6 rounded-2xl shadow-sm border text-center">
          <div class="text-3xl font-bold text-primary-500 mb-2">892</div>
          <div class="text-gray-600">Предложений</div>
        </div>
        <div class="bg-white p-6 rounded-2xl shadow-sm border text-center">
          <div class="text-3xl font-bold text-primary-500 mb-2">124</div>
          <div class="text-gray-600">Сделок сегодня</div>
        </div>
      </div>
    </div>

    <!-- Requests Section -->
    <section id="requests" class="container mx-auto px-4 pb-20">
      <div class="flex flex-col md:flex-row md:items-center justify-between mb-8">
        <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4 md:mb-0">
          Актуальные запросы покупателей
        </h2>
        <div class="flex space-x-4">
          <select
            v-model="selectedCategory"
            class="px-4 py-2.5 bg-white border border-gray-300 rounded-xl text-gray-700 focus:outline-none focus:ring-2 focus:ring-primary-500 focus:border-transparent cursor-pointer"
            @change="handleCategoryChange"
          >
            <option value="all">Все категории</option>
            <option v-for="category in categoryOptions" :key="category.key" :value="category.key">
              {{ category.label }}
            </option>
          </select>
          <button class="px-4 py-2.5 bg-gray-100 text-gray-700 rounded-xl hover:bg-gray-200 transition-colors cursor-pointer">
            🔍 Фильтры
          </button>
        </div>
      </div>

      <div v-if="loading" class="text-center py-12">
        <div class="inline-block animate-spin rounded-full h-12 w-12 border-4 border-primary-500 border-t-transparent"></div>
        <p class="mt-4 text-gray-600">Загружаем запросы...</p>
      </div>

      <div v-else class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <RequestCard
          v-for="request in displayedRequests"
          :key="request.id"
          :request="request"
        />
      </div>

      <div v-if="!loading && displayedRequests.length === 0" class="text-center py-12">
        <div class="text-gray-400 mb-4">
          <svg class="w-24 h-24 mx-auto" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9.172 16.172a4 4 0 015.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>
          </svg>
        </div>
        <h3 class="text-xl font-semibold text-gray-700 mb-2">Пока нет запросов</h3>
        <p class="text-gray-500 mb-6">Будьте первым, кто создаст запрос!</p>
        <button
          @click="router.push('/create-request')"
          class="px-6 py-3 bg-primary-500 text-white font-medium rounded-xl hover:bg-primary-600 transition-colors cursor-pointer"
        >
          Создать первый запрос
        </button>
      </div>

      <div v-if="hasMoreRequests && !loading && displayedRequests.length > 0" class="text-center mt-12">
        <button
          @click="loadMoreRequests"
          class="px-8 py-3 bg-white text-primary-600 font-medium rounded-xl border-2 border-primary-500 hover:bg-primary-50 transition-colors cursor-pointer hover:-translate-y-0.5 hover:shadow-lg"
          :disabled="loadingMore"
        >
          <span v-if="loadingMore" class="flex items-center justify-center">
            <svg class="animate-spin -ml-1 mr-3 h-5 w-5 text-primary-500" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
              <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
              <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
            </svg>
            Загрузка...
          </span>
          <span v-else>
            Показать еще ({{ remainingRequestsCount }})
          </span>
        </button>
      </div>
    </section>

    <!-- CTA Section -->
    <section class="bg-primary-500 text-white py-16">
      <div class="container mx-auto px-4 text-center">
        <h2 class="text-3xl md:text-4xl font-bold mb-6">Начни покупать по своей цене уже сегодня!</h2>
        <p class="text-xl opacity-90 mb-10 max-w-2xl mx-auto">
          Присоединяйся к тысячам пользователей, которые уже экономят на покупках
        </p>
        <button
          @click="router.push('/register')"
          class="px-10 py-4 bg-white text-primary-600 text-xl font-bold rounded-xl hover:bg-gray-100 transition-colors shadow-2xl hover:shadow-3xl cursor-pointer"
        >
          Бесплатная регистрация
        </button>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import RequestCard from '../components/cards/RequestCard.vue'

const router = useRouter()

// Конфигурация
const ITEMS_PER_PAGE = 9

// Категории для фильтрации
const categoryOptions = [
  { key: 'all', label: 'Все категории' },
  { key: 'electronics', label: 'Электроника' },
  { key: 'clothes', label: 'Одежда и обувь' },
  { key: 'realty', label: 'Недвижимость' },
  { key: 'services', label: 'Услуги' },
  { key: 'vehicles', label: 'Транспорт' },
  { key: 'hobbies', label: 'Хобби и отдых' },
  { key: 'other', label: 'Другое' }
]

// Исходные данные (много карточек)
const allRequests = ref([
  {
    id: 1,
    title: 'iPhone 15 Pro 256GB',
    description: 'Ищу новый или б/у iPhone 15 Pro в отличном состоянии. Цвет не важен, главное чтобы батарея была в хорошем состоянии.',
    price: 90000,
    category: 'electronics',
    location: 'Казань',
    date: 'Сегодня',
    userName: 'Алексей',
    userInitials: 'А',
    offersCount: 5
  },
  {
    id: 2,
    title: 'Кроссовки Nike Air Max 270',
    description: 'Нужны кроссовки Nike Air Max 270, размер 42. В хорошем состоянии, без сильных потертостей.',
    price: 8000,
    category: 'clothes',
    location: 'Москва',
    date: 'Вчера',
    userName: 'Марина',
    userInitials: 'М',
    offersCount: 3
  },
  {
    id: 3,
    title: 'Игровой ноутбук с RTX 4060',
    description: 'Нужен игровой ноутбук с минимум 16 ГБ ОЗУ, видеокарта RTX 4060, процессор i7 или Ryzen 7.',
    price: 120000,
    category: 'electronics',
    location: 'Москва',
    date: '2 часа назад',
    userName: 'Иван',
    userInitials: 'И',
    offersCount: 7
  },
  {
    id: 4,
    title: 'Горный велосипед',
    description: 'Ищу горный велосипед для поездок по бездорожью. Рост 180 см. Бюджет до 35000 рублей.',
    price: 35000,
    category: 'vehicles',
    location: 'Екатеринбург',
    date: '2 дня назад',
    userName: 'Дмитрий',
    userInitials: 'Д',
    offersCount: 4
  },
  {
    id: 5,
    title: '1-комнатная квартира в центре',
    description: 'Ищу 1-комнатную квартиру для аренды в центре города. Долгосрочно. Без посредников.',
    price: 30000,
    category: 'realty',
    location: 'Санкт-Петербург',
    date: 'Сегодня',
    userName: 'Ольга',
    userInitials: 'О',
    offersCount: 12
  },
  {
    id: 6,
    title: 'Ремонт ноутбука Dell',
    description: 'Нужен мастер по ремонту ноутбуков. Dell Inspiron не включается после падения. Срочно!',
    price: 5000,
    category: 'services',
    location: 'Новосибирск',
    date: 'Сегодня',
    userName: 'Сергей',
    userInitials: 'С',
    offersCount: 4
  },
  {
    id: 7,
    title: 'Акустическая гитара Yamaha',
    description: 'Ищу акустическую гитару для начинающего. Желательно Yamaha или Fender. Бюджет до 15000.',
    price: 15000,
    category: 'hobbies',
    location: 'Краснодар',
    date: '3 дня назад',
    userName: 'Иван',
    userInitials: 'И',
    offersCount: 2
  },
  {
    id: 8,
    title: 'Щенок лабрадора с документами',
    description: 'Ищу щенка лабрадора, возраст до 4 месяцев, с документами РКФ. Важно здоровье и хорошая наследственность.',
    price: 45000,
    category: 'other',
    location: 'Санкт-Петербург',
    date: 'Вчера',
    userName: 'Анна',
    userInitials: 'А',
    offersCount: 6
  },
  {
    id: 9,
    title: 'Зимние шины R17 225/55',
    description: 'Нужны 4 зимние шины R17 225/55, состояние новое или б/у с остатком протектора не менее 6 мм.',
    price: 30000,
    category: 'vehicles',
    location: 'Екатеринбург',
    date: 'Неделю назад',
    userName: 'Андрей',
    userInitials: 'А',
    offersCount: 8
  },
  // Дополнительные карточки (с 10 по 18)
  {
    id: 10,
    title: 'PlayStation 5',
    description: 'Ищу PlayStation 5 в хорошем состоянии, с гарантией и чеком. Рассмотрю любые игры в комплекте.',
    price: 45000,
    category: 'electronics',
    location: 'Москва',
    date: 'Сегодня',
    userName: 'Михаил',
    userInitials: 'М',
    offersCount: 3
  },
  {
    id: 11,
    title: 'Куртка зимняя мужская',
    description: 'Нужна теплая зимняя куртка, размер 52-54. Предпочтительно бренды The North Face, Columbia.',
    price: 15000,
    category: 'clothes',
    location: 'Новосибирск',
    date: '2 дня назад',
    userName: 'Павел',
    userInitials: 'П',
    offersCount: 5
  },
  {
    id: 12,
    title: 'Фотоаппарат Canon EOS R6',
    description: 'Ищу зеркальный фотоаппарат Canon EOS R6 с объективом. Рассмотрю разные комплектации.',
    price: 180000,
    category: 'electronics',
    location: 'Санкт-Петербург',
    date: 'Вчера',
    userName: 'Олег',
    userInitials: 'О',
    offersCount: 2
  },
  {
    id: 13,
    title: 'Диван угловой новый',
    description: 'Нужен угловой диван для гостиной, длина не менее 3 метров. Рассмотрю варианты с доставкой.',
    price: 60000,
    category: 'other',
    location: 'Казань',
    date: 'Сегодня',
    userName: 'Елена',
    userInitials: 'Е',
    offersCount: 7
  },
  {
    id: 14,
    title: 'Услуги дизайнера интерьера',
    description: 'Ищу дизайнера для разработки дизайн-проекта квартиры 65 кв.м. Срок - 2 недели.',
    price: 40000,
    category: 'services',
    location: 'Москва',
    date: '3 дня назад',
    userName: 'Арина',
    userInitials: 'А',
    offersCount: 4
  },
  {
    id: 15,
    title: 'Скейтборд для начинающего',
    description: 'Ищу скейтборд для ребенка 10 лет. Нужен полный комплект в хорошем состоянии.',
    price: 5000,
    category: 'hobbies',
    location: 'Екатеринбург',
    date: 'Вчера',
    userName: 'Артем',
    userInitials: 'А',
    offersCount: 3
  },
  {
    id: 16,
    title: 'Смарт-часы Apple Watch Series 8',
    description: 'Ищу Apple Watch Series 8, размер 45mm. Рассмотрю любые цвета, главное - хорошее состояние.',
    price: 30000,
    category: 'electronics',
    location: 'Москва',
    date: 'Сегодня',
    userName: 'Дарья',
    userInitials: 'Д',
    offersCount: 6
  },
  {
    id: 17,
    title: 'Книги по программированию',
    description: 'Ищу книги по Vue.js, TypeScript и современному фронтенду. Рассмотрю как новые, так и б/у.',
    price: 5000,
    category: 'other',
    location: 'Онлайн',
    date: 'Неделю назад',
    userName: 'Сергей',
    userInitials: 'С',
    offersCount: 2
  },
  {
    id: 18,
    title: 'Услуги массажиста',
    description: 'Ищу профессионального массажиста для регулярных сеансов. Рассмотрю выезд на дом.',
    price: 2000,
    category: 'services',
    location: 'Санкт-Петербург',
    date: 'Сегодня',
    userName: 'Наталья',
    userInitials: 'Н',
    offersCount: 5
  }
])

const selectedCategory = ref<string>('all')
const loading = ref<boolean>(true)
const loadingMore = ref<boolean>(false)
const displayCount = ref<number>(ITEMS_PER_PAGE)

// Фильтруем запросы по категории
const filteredRequests = computed(() => {
  if (selectedCategory.value === 'all') {
    return allRequests.value
  }
  return allRequests.value.filter(request => request.category === selectedCategory.value)
})

// Отображаемые запросы (с учетом пагинации)
const displayedRequests = computed(() => {
  return filteredRequests.value.slice(0, displayCount.value)
})

// Проверяем, есть ли еще запросы для загрузки
const hasMoreRequests = computed(() => {
  return displayCount.value < filteredRequests.value.length
})

// Количество оставшихся запросов
const remainingRequestsCount = computed(() => {
  return filteredRequests.value.length - displayCount.value
})

// Загрузка дополнительных запросов
const loadMoreRequests = async () => {
  loadingMore.value = true

  // Имитация загрузки (можно убрать в реальном приложении)
  await new Promise(resolve => setTimeout(resolve, 500))

  // Увеличиваем количество отображаемых карточек
  displayCount.value += ITEMS_PER_PAGE

  loadingMore.value = false
}

// Обработчик изменения категории
const handleCategoryChange = () => {
  // Сбрасываем счетчик отображения при смене категории
  displayCount.value = ITEMS_PER_PAGE
}

onMounted(() => {
  // Имитация загрузки данных
  setTimeout(() => {
    loading.value = false
  }, 1000)
})
</script>
