<script setup>
import { ref, onMounted } from 'vue'

const quote = ref([{
  quote: 'The greatest glory in living lies not in never falling, but in rising every time we fall.',
  author: 'Nelson Mandela'
},
{
  quote: 'The way to get started is to quit talking and begin doing.',
  author: 'Walt Disney'
},
{
  quote: 'Your time is limited, so don\'t waste it living someone else\'s life.',
  author: 'Steve Jobs'
},
{
  quote: 'If life were predictable it would cease to be life, and be without flavor.',
  author: 'Eleanor Roosevelt'
},
{
  quote: 'If you set your goals ridiculously high and it\'s a failure, you will fail above everyone else\'s success.',
  author: 'James Cameron'
},
{
  quote: 'Life is what happens when you\'re busy making other plans.',
  author: 'John Lennon'
},
{
  quote: 'Spread love everywhere you go. Let no one ever come to you without leaving happier.',
  author: 'Mother Teresa'
}
])

const currentQuote = ref({ quote: '', author: '' })


const generateQuote = () => {
  const randomIndex = Math.floor(Math.random() * quote.value.length)
  currentQuote.value = quote.value[randomIndex]
}

onMounted(() => {
  generateQuote()
})


</script>

<template>
  <div class="quote-generator">
    <p>{{ currentQuote.quote }}</p>
    <p>- {{ currentQuote.author }}</p>
    <button @click="generateQuote">Generate Quote</button>
  </div>
</template>

<style scoped>
.quote-generator {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

</style>
