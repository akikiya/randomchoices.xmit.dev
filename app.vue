<template>
  <div id="app">
    <header>
      <h1>RandomChoices</h1>
      <p>Make decisions easily with random selection</p>
    </header>
    <section id="input-section">
      <input type="text" placeholder="Enter your choices (one at a time)" v-model="inputValue">
      <button type="button" @click="addChoice">Add</button>
    </section>
    <section id="choices-section">
      <header>
        <h2>Your Choices</h2>
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
