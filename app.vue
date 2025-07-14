<template>
  <div id="app">
    <header>
      <h1>Random Choices</h1>
      <p>Make decisions easily with random selection</p>
    </header>
    <form action="javascript:void(0);" @submit.prevent="addChoice" id="input-section">
      <input type="text" placeholder="Enter your choices (one at a time)" v-model="inputValue">
      <button type="submit">Add</button>
    </form>
    <section id="choices-section">
      <header>
        <h2>Your Choices</h2>
        <p v-if="choices.length > 1">You have {{ choices.length }} choices</p>
        <p v-else-if="choices.length === 1">You have {{ choices.length }} choice</p>
        <p v-else>You have no choices</p>
      </header>
      <section class="container">
        <p v-if="!choices.length">Your choices will appear here</p>
        <ul v-else>
          <li class="choice-item" v-for="choice in choices" :key="choice">
            <div class="content">{{ choice }}</div>
            <button type="button" @click="choices = choices.filter(c => c !== choice)">Remove</button>
          </li>
        </ul>
      </section>
    </section>
    <section id="picker-section">
      <header>
        <h2>Your Random Choice</h2>
      </header>
      <section class="container">
        <p v-if="!randomChoice">
          Click the button below to get a random choice
        </p>
        <p v-else>
          {{ randomChoice }}
        </p>
        <button type="button" @click="pickRandom">
          Pick Random
        </button>
      </section>
    </section>
  </div>
</template>

<script setup lang="ts">
import "normalize.css"
import { ref } from 'vue'

const inputValue = ref('')
const choices = ref<string[]>([])
const randomChoice = ref('')

function addChoice() {
  if (!inputValue.value) return
  if (choices.value.includes(inputValue.value)) {
    inputValue.value = ''
    return
  }
  choices.value.push(inputValue.value)
  inputValue.value = ''
}
function pickRandom() {
  if (!choices.value.length) return
  const randomIndex = Math.floor(Math.random() * choices.value.length)
  randomChoice.value = choices.value[randomIndex]
}
</script>

<style>
:root {
  --primary-color: #6c63ff;
  --secondary-color: #f5f5f5;
  --text-color: #333;
  --border-radius: 8px;
  --box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  --transition: all 0.3s ease;
}

body {
  font-family: 'Inter', 'Helvetica Neue', Arial, sans-serif;
  line-height: 1.6;
  color: var(--text-color);
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
  min-height: 100vh;
  padding: 20px;
}

#app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: white;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

header {
  text-align: center;
  margin-bottom: 30px;
  padding-bottom: 20px;
  border-bottom: 1px solid #eee;
}

h1 {
  color: var(--primary-color);
  font-size: 2.5rem;
  margin-bottom: 5px;
}

h2 {
  font-size: 1.5rem;
  color: var(--primary-color);
  margin-bottom: 15px;
}

section {
  margin-bottom: 30px;
}

#input-section {
  display: flex;
  gap: 10px;
  margin-bottom: 30px;
}

input[type="text"] {
  flex: 1;
  padding: 12px 15px;
  border: 2px solid #eee;
  border-radius: var(--border-radius);
  font-size: 1rem;
  transition: var(--transition);
}

input[type="text"]:focus {
  border-color: var(--primary-color);
  outline: none;
  box-shadow: 0 0 0 3px rgba(108, 99, 255, 0.2);
}

button {
  background-color: var(--primary-color);
  color: white;
  border: none;
  border-radius: var(--border-radius);
  padding: 12px 20px;
  font-size: 1rem;
  cursor: pointer;
  transition: var(--transition);
}

button:hover {
  background-color: #5a52d5;
  transform: translateY(-2px);
  box-shadow: 0 6px 10px rgba(0, 0, 0, 0.15);
}

.container {
  background-color: var(--secondary-color);
  padding: 20px;
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow);
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.choice-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: white;
  padding: 12px 15px;
  margin-bottom: 10px;
  border-radius: var(--border-radius);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  transition: var(--transition);
}

.choice-item:hover {
  transform: translateX(5px);
}

.choice-item:last-child {
  margin-bottom: 0;
}

.content {
  font-weight: 500;
}

.choice-item button {
  background-color: #ff6b6b;
  padding: 8px 12px;
  font-size: 0.85rem;
}

.choice-item button:hover {
  background-color: #ee5253;
}

#picker-section .container {
  text-align: center;
}

#picker-section p {
  font-size: 1.2rem;
  margin-bottom: 20px;
}

#picker-section button {
  margin-top: 10px;
  padding: 15px 30px;
  font-size: 1.1rem;
  background-color: #4cd964;
}

#picker-section button:hover {
  background-color: #43c558;
}

@media (max-width: 600px) {
  #input-section {
    flex-direction: column;
  }

  button {
    width: 100%;
  }
}
</style>
