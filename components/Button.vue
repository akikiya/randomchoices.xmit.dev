<template>
  <button 
    :type="type"
    :class="[
      'px-4 py-2 rounded-lg transition-colors',
      variant === 'primary' ? 'bg-indigo-600 text-white hover:bg-indigo-500' : '',
      variant === 'secondary' ? 'bg-gray-200 text-gray-700 hover:bg-gray-300' : '',
      variant === 'danger' ? 'text-red-500 hover:bg-gray-100' : '',
      size === 'sm' ? 'text-sm px-2 py-1' : '',
      size === 'lg' ? 'text-lg px-6 py-3' : '',
      disabled ? 'opacity-50 cursor-not-allowed' : '',
      fullWidth ? 'w-full' : ''
    ]"
    :disabled="disabled"
    @click="$emit('click', $event)"
  >
    <slot></slot>
  </button>
</template>

<script setup lang="ts">
interface Props {
  type?: 'button' | 'submit' | 'reset'
  variant?: 'primary' | 'secondary' | 'danger'
  size?: 'sm' | 'md' | 'lg'
  disabled?: boolean
  fullWidth?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  type: 'button',
  variant: 'primary',
  size: 'md',
  disabled: false,
  fullWidth: false
})

defineEmits(['click'])
</script>
