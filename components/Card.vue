<template>
  <div class="card">
    <header class="card__header">
      <slot name="header"></slot>
    </header>
    <div class="card__content">
      <slot name="content"></slot>
    </div>
    <div class="card__action">
      <slot name="action"></slot>
    </div>
  </div>
</template>

<script setup lang="ts">
defineSlots<{
  header: (props: {}) => any
  content: (props: {}) => any
  action: (props: {}) => any
}>()
</script>

<style>
.card {
  @apply bg-white rounded-lg shadow-md p-6 m-4;
}
.card__header {
  @apply text-xl font-bold;
}
.card__content {
  @apply my-4 ;
}
.card__action {
  @apply text-center;
}
.card__action button {
  @apply m-1 px-4 py-2 rounded-lg;
  @apply bg-indigo-600 text-white;
  @apply hover:bg-indigo-500 transition-colors;
}
.card__action button:disabled {
  @apply opacity-50 cursor-not-allowed;
  @apply hover:bg-indigo-600;
}
</style>