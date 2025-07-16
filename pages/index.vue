<template>
    <div id="app" class="min-h-screen bg-gray-50 py-8 px-4 sm:px-6 lg:px-8">
        <div class="max-w-3xl mx-auto">
            <!-- Header -->
            <header class="text-center mb-10">
                <h1 class="text-4xl font-bold text-indigo-600 mb-2">Decision Maker</h1>
                <p class="text-lg text-gray-600">Let randomness decide for you when you can't choose</p>
            </header>

            <!-- Add Option Form -->
            <form action="javascript:void(0)" @submit.prevent="addOption" class="mb-8 flex gap-2">
                <input type="text" placeholder="Type an option here..." v-model="optionInput"
                    class="flex-1 rounded-lg border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 px-4 py-2">
                <Button type="submit" variant="primary">Add Option</Button>
            </form>

            <!-- Options List -->
            <Card>
                <template #header>
                    <div class="flex justify-between items-center">
                        <h2>Your Options</h2>
                        <div class="text-sm font-medium text-gray-500 bg-gray-100 px-3 py-1 rounded-full">
                            {{ optionsList.size }} {{ optionsList.size > 1 ? 'options' : 'option' }}
                        </div>
                    </div>
                </template>
                <template #content>
                    <ul v-if="optionsList.size > 0" class="space-y-2 border-l-4 border-indigo-200 pl-4">
                        <li v-for="option in optionsList" :key="option" class="flex justify-between items-center">
                            <div class="font-medium">{{ option }}</div>
                            <Button @click="optionsList.delete(option)" variant="danger" size="sm">Remove</Button>
                        </li>
                    </ul>
                    <p v-else class="text-center text-gray-500 italic">Add some options to get started</p>
                </template>
                <template #action>
                    <Button 
                        @click="optionsList.clear()" 
                        variant="secondary" 
                        :disabled="optionsList.size === 0"
                    >
                        Clear All
                    </Button>
                </template>
            </Card>

            <!-- Random Option Section -->
            <Card>
                <template #header>
                    <h2>The Decision</h2>
                </template>
                <template #content>
                    <p v-if="selectedOption" class="bg-indigo-100 p-4 rounded-lg text-center font-bold text-indigo-800">
                        {{ selectedOption }}
                    </p>
                    <p v-else class="text-center text-gray-600">
                        <template v-if="optionsList.size === 0">
                            Please add some options first
                        </template>
                        <template v-else>
                            Click the button below and let fate decide!
                        </template>
                    </p>
                </template>
                <template #action>
                    <Button @click="makeDecision" :disabled="optionsList.size === 0">Make Decision</Button>
                </template>
            </Card>
        </div>
    </div>
</template>

<script setup lang="ts">
const optionInput = ref('');
const optionsList = ref(new Set<string>())
const selectedOption = ref('');

function addOption() {
    if (!optionInput.value.trim()) return;
    optionsList.value.add(optionInput.value);
    optionInput.value = '';
}
function makeDecision() {
    if (optionsList.value.size === 0) return;
    const options = Array.from(optionsList.value);
    const randomIndex = Math.floor(Math.random() * options.length);
    selectedOption.value = options[randomIndex];
}
</script>

