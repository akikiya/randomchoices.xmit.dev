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
                <Button type="submit" variant="primary">Add</Button>
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
                            <Button @click="choices.delete(choice)" variant="danger" size="sm">Remove</Button>
                        </li>
                    </ul>
                    <p v-else class="text-center">Your choices will appear here</p>
                </template>
                <template #action>
                    <Button 
                        @click="choices.clear()" 
                        variant="secondary" 
                        :disabled="choices.size === 0"
                    >
                        Clear All
                    </Button>
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
                    <Button @click="selectChoice" :disabled="choices.size === 0">Select Random</Button>
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

