<template>
  <div class="w-full h-full flex justify-center items-center">
    <div class="max-w-xs w-full flex flex-col">
      <p class="w-3/4 p-4 rounded-2xl bg-teal-800 text-white self-start">{{ setup }}</p>
      <p v-if="reveal" class="w-3/4 mt-2 p-4 rounded-2xl bg-red-800 text-white self-end">{{ delivery }}</p>
      <button
        role="button"
        name="Tell Me!"
        @click="revealJoke"
        class="bg-green col-span-1 rounded-lg py-2 hover:opacity-90 w-full mx-auto mt-4"
      >
        {{ buttonText }}
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const setup = ref(null)
const delivery = ref(null)
const reveal = ref(false)
const buttonText = ref('Tell Me!')

function revealJoke() {
  if (!reveal.value) {
    reveal.value = true
    buttonText.value = 'Another'
  } else {
    reveal.value = false
    buttonText.value = 'Tell me!'
    getJoke()
  }
}

function getJoke() {
  fetch('https://v2.jokeapi.dev/joke/christmas')
    .then(data => data.json())
    .then(data => {
      console.log(data.setup, data.delivery)
      setup.value = data.setup
      delivery.value = data.delivery
    })
}

getJoke()
</script>
