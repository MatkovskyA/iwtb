<template>
  <button
    :class="buttonClasses"
    :type="type"
    :disabled="disabled || loading"
    :aria-busy="loading"
    :aria-disabled="disabled"
    @click="handleClick"
  >
    <span v-if="loading" class="ui-button__loader" aria-hidden="true"></span>
    <span v-else class="ui-button__content">
      <slot />
    </span>
  </button>
</template>

<script setup lang="ts">
import { computed } from 'vue'

interface Props {
  variant?: 'primary' | 'secondary' | 'outline' | 'text'
  size?: 'xs' | 's' | 'm' | 'l' | 'xl'
  type?: 'button' | 'submit' | 'reset'
  disabled?: boolean
  loading?: boolean
  fullWidth?: boolean
  pill?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  variant: 'primary',
  size: 'm',
  type: 'button',
  disabled: false,
  loading: false,
  fullWidth: false,
  pill: false
})

const emit = defineEmits<{
  click: [event: MouseEvent]
}>()

const handleClick = (event: MouseEvent): void => {
  if (!props.disabled && !props.loading) {
    emit('click', event)
  }
}

const buttonClasses = computed(() => [
  'ui-button',
  `ui-button__${props.variant}`,
  `ui-button__${props.size}`,
  {
    'ui-button__disabled': props.disabled,
    'ui-button__loading': props.loading,
    'ui-button__full-width': props.fullWidth,
    'ui-button__pill': props.pill
  }
])
</script>

<style scoped>
.ui-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 12px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s ease;
  border: 2px solid transparent;
  font-family: inherit;
  touch-action: manipulation;
  -webkit-tap-highlight-color: transparent;
  user-select: none;
}

/* Варианты кнопок */
.ui-button__primary {
  background-color: var(--color-primary, #42b883);
  color: white;
  border-color: var(--color-primary, #42b883);
}

.ui-button__primary:hover:not(.ui-button__disabled):not(.ui-button__loading) {
  background-color: var(--color-primary-dark, #3aa876);
  border-color: var(--color-primary-dark, #3aa876);
}

.ui-button__secondary {
  background-color: var(--color-secondary, #f5f5f5);
  color: var(--color-text, #2c3e50);
  border-color: var(--color-secondary, #f5f5f5);
}

.ui-button__outline {
  background-color: transparent;
  color: var(--color-primary, #42b883);
  border-color: var(--color-primary, #42b883);
}

.ui-button__text {
  background-color: transparent;
  color: var(--color-primary, #42b883);
  border: none;
  padding: 0;
  min-height: auto;
}

/* Размеры */
.ui-button__xs {
  padding: 8px 16px;
  font-size: 14px;
  min-height: 44px;
}

.ui-button__s {
  padding: 12px 20px;
  font-size: 15px;
  min-height: 48px;
}

.ui-button__m {
  padding: 16px 24px;
  font-size: 16px;
  min-height: 52px;
}

.ui-button__l {
  padding: 20px 28px;
  font-size: 17px;
  min-height: 56px;
}

.ui-button__xl {
  padding: 24px 32px;
  font-size: 18px;
  min-height: 60px;
}

/* Модификаторы состояния */
.ui-button__disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.ui-button__loading {
  cursor: wait;
}

.ui-button__full-width {
  width: 100%;
}

.ui-button__pill {
  border-radius: 9999px;
}

/* Лоадер */
.ui-button__loader {
  width: 20px;
  height: 20px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  border-top-color: white;
  animation: spin 0.8s linear infinite;
}

.ui-button__secondary .ui-button__loader,
.ui-button__outline .ui-button__loader {
  border: 2px solid rgba(66, 184, 131, 0.3);
  border-top-color: #42b883;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

/* Hover/Active состояния */
@media (hover: hover) {
  .ui-button:not(.ui-button__disabled):not(.ui-button__loading):hover {
    transform: translateY(-1px);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  }
}

.ui-button:not(.ui-button__disabled):not(.ui-button__loading):active {
  transform: translateY(0);
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}
</style>
