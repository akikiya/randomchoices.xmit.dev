<template>
    <div id="app" class="min-h-screen bg-gray-50 py-8 px-4 sm:px-6 lg:px-8">
        <div class="max-w-3xl mx-auto">
            <!-- Header -->
            <header class="text-center mb-10">
                <h1 class="text-4xl font-bold text-indigo-600 mb-2">Random Choices</h1>
                <p class="text-lg text-gray-600">Make decisions easily with random selection</p>
            </header>

            <!-- Add Choice Form -->
            <form action="javascript:void(0)" @submit.prevent="addChoice" class="mb-8 flex gap-2">
                <input 
                    type="text" 
                    placeholder="Enter a choice" 
                    v-model="input"
                    class="flex-1 rounded-lg border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 px-4 py-2"
                >
                <button 
                    type="submit"
                    class="primary-button"
                >
                    Add
                </button>
            </form>

            <!-- Choices List -->
            <div class="card mb-8">
                <header class="card-header flex justify-between items-center">
                    <h2 class="card-title">Your Choices</h2>
                    <div class="text-sm font-medium text-gray-500 bg-gray-100 px-3 py-1 rounded-full">
                        {{ choices.size }} {{ choices.size > 1 ? 'choices' : 'choice' }}
                    </div>
                </header>
                <div>
                    <ul v-if="choices.size > 0" class="space-y-2 mb-4">
                        <li 
                            v-for="choice in choices" 
                            :key="choice"
                            class="choice-item"
                        >
                            <div class="font-medium">{{ choice }}</div>
                            <button 
                                @click="choices.delete(choice)"
                                class="text-red-500 hover:text-red-700 transition-colors text-sm py-1 px-2"
                            >
                                Remove
                            </button>
                        </li>
                    </ul>
                    <p v-else class="text-center text-gray-500 py-6">Your choices will appear here</p>
                    <div class="text-center">
                        <button 
                            @click="choices.clear()"
                            class="secondary-button"
                            :disabled="choices.size === 0"
                            :class="{'opacity-50 cursor-not-allowed': choices.size === 0}"
                        >
                            Clear All
                        </button>
                    </div>
                </div>
            </div>

            <!-- Random Choice -->
            <div class="card">
                <header class="card-header">
                    <h2 class="card-title">Random Choice</h2>
                </header>
                <div class="card-content">
                    <p v-if="choices.size === 0" class="text-gray-500 mb-6 py-4">
                        No choices to select from
                    </p>
                    <p v-else-if="!selectedChoice" class="text-gray-600 mb-6 py-4">
                        Click the button below to select a random choice
                    </p>
                    <p v-else class="text-2xl font-bold text-indigo-600 mb-6 py-6 bg-indigo-50 rounded-lg">
                        {{ selectedChoice }}
                    </p>
                    <button 
                        @click="selectChoice"
                        class="primary-button"
                        :disabled="choices.size === 0"
                        :class="{'opacity-50 cursor-not-allowed': choices.size === 0}"
                    >
                        Select Random
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
const input = ref('');
const choices = ref(new Set<string>())
const selectedChoice = ref('');

function addChoice() {
    if (!input.value) return;
    choices.value.add(input.value);
    input.value = '';
}
function selectChoice() {
    if (choices.value.size === 0) return;
    const arr = Array.from(choices.value);
    const randomIndex = Math.floor(Math.random() * arr.length);
    selectedChoice.value = arr[randomIndex];
}
</script>

<style>
.card {
  @apply bg-white rounded-lg shadow-md p-6;
}

.card-header {
  @apply mb-4 pb-3 border-b border-gray-200;
}

.card-title {
  @apply text-2xl font-semibold text-gray-800;
}

.card-content {
  @apply text-center;
}

.primary-button {
  @apply bg-indigo-600 text-white px-6 py-2 rounded-lg hover:bg-indigo-700 transition-colors font-medium;
}

.secondary-button {
  @apply text-gray-600 hover:text-gray-800 text-sm border border-gray-300 rounded-lg px-4 py-2 transition-colors;
}

.choice-item {
  @apply flex justify-between items-center p-3 bg-gray-50 rounded-md hover:bg-gray-100 transition-colors;
}
</style>