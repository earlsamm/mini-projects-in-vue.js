<script setup>
import { ref, onMounted, watch } from 'vue'

let display = ref('0')
let buttons = ['7', '8', '9', '/', '4', '5', '6', '*', '1', '2', '3', '-', 'C', '0', '=', '+']

let onButtonClick = (button) => {
  if (button === 'C') {
    display.value = '0'
  } else if (button === '=') {
    display.value = eval(display.value)
  } else {
    display.value = display.value === '0' ? button : display.value + button
  }
}

// Prevent the default behavior of the Enter key
window.addEventListener('keydown', (event) => {
  if (event.key === 'Enter') {
    event.preventDefault()
  }
})

// Handle the keydown event
window.addEventListener('keydown', (event) => {
  if (event.key === 'Enter') {
    onButtonClick('=')
  } else if (buttons.includes(event.key)) {
    onButtonClick(event.key)
  }
})

// Focus the display element when the component is mounted
onMounted(() => {
  document.querySelector('.display').focus()
})

// Focus the display element when the display value changes
watch(display, () => {
  document.querySelector('.display').focus()
})

// Focus the display element when a button is clicked
</script>
<template>
  <div class="calculator">
    <div class="display">{{ display }}</div>
    <div class="buttons">
      <button v-for="button in buttons" :key="button" @click="onButtonClick(button)">
        {{ button }}
      </button>
    </div>
  </div>
</template>
<style scoped>
.calculator {
  width: 200px;
  margin: 50px auto;
  padding: 10px;
  border: 2px solid #ccc;
  border-radius: 10px;
  box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.2);
  font-family: Arial, sans-serif;
}

.display {
  height: 40px;
  margin-bottom: 10px;
  padding: 0 10px;
  text-align: right;
  font-size: 18px;
  line-height: 40px;
  background: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 5px;
  overflow: hidden;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 5px;
}

button {
  height: 40px;
  font-size: 16px;
  background: #f1f1f1;
  border: 1px solid #ddd;
  border-radius: 5px;
  cursor: pointer;
  transition: background 0.3s;
}

button:hover {
  background: #e0e0e0;
}
</style>
