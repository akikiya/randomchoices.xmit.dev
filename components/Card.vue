<template>
  <div class="bg-white rounded-lg shadow-md p-6 m-4">
    <header class="text-xl font-bold mb-4">
      <slot name="header"></slot>
    </header>
    <div class="my-4">
      <slot name="content"></slot>
    </div>
    <div class="text-center">
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
