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
                <input type="text" placeholder="Enter a choice" v-model="input"
                    class="flex-1 rounded-lg border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 px-4 py-2">
                <button type="submit" class="bg-indigo-600 text-white rounded-lg px-4 py-2 hover:bg-indigo-500 transition-colors">
                    Add
                </button>
            </form>

            <!-- Choices List -->
            <Card>
                <template #header>
                    <div class="flex justify-between items-center">
                        <h2>Your Choices</h2>
                        <div class="text-sm font-medium text-gray-500 bg-gray-100 px-3 py-1 rounded-full">
                            {{ choices.size }} {{ choices.size > 1 ? 'choices' : 'choice' }}
                        </div>
                    </div>
                </template>
                <template #content>
                    <ul v-if="choices.size > 0" class="space-y-2 border-l-4 border-indigo-200 pl-4">
                        <li v-for="choice in choices" :key="choice" class="flex justify-between items-center">
                            <div class="font-medium">{{ choice }}</div>
                            <button @click="choices.delete(choice)"
                                class="text-red-500 hover:text-red-700 transition-colors text-sm py-1 px-2">
                                Remove
                            </button>
                        </li>
                    </ul>
                    <p v-else class="text-center">Your choices will appear here</p>
                </template>
                <template #action>
                    <button @click="choices.clear()" class="secondary-button" :disabled="choices.size === 0"
                        :class="{ 'opacity-50 cursor-not-allowed': choices.size === 0 }">
                        Clear All
                    </button>
                </template>
            </Card>

            <!-- Random Choice Section -->
            <Card>
                <template #header>
                    <h2>Random Choice</h2>
                </template>
                <template #content>
                    <p v-if="selectedChoice" class="bg-indigo-100 p-4 rounded-lg text-center">
                        {{ selectedChoice }}
                    </p>
                    <p v-else class="text-center">
                        <template v-if="choices.size === 0">
                            No choices to select from
                        </template>
                        <template v-else>
                            Click the button below to select a random choice
                        </template>
                    </p>
                </template>
                <template #action>
                    <button @click="selectChoice" :disabled="choices.size === 0">Select Random</button>
                </template>
            </Card>
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
