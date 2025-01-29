<script setup>
import GithubUserProfile from './GithubUserProfile.vue'
import FormValidation from './FormValidation.vue'
import RandomQuoteGenerator from './RandomQuoteGenerator.vue'
import SimpleCalculator from './SimpleCalculator.vue'
import TodoApp from './TodoApp.vue'
</script>
<template>
  <div class="row px-5 mt-5">
    <div class="col-md-6">
      <h1 class="title">Fetch Github User Data</h1>
      <GithubUserProfile />
    </div>
    <div class="col-md-6">
      <h1 class="title">Form Validation</h1>
      <FormValidation />
    </div>
    <div class="col-md-6">
      <h1 class="title">Simple Calculator</h1>
      <SimpleCalculator />
    </div>

    <div class="col-md-6">
      <h1 class="title">Random Quote Generator</h1>
      <RandomQuoteGenerator />
    </div>

    <div class="col-md-6">
      <h1 class="title">Todo App</h1>
      <TodoApp />
    </div>
  </div>
</template>
<style scoped>
.title {
  font-size: 2rem;
  margin-bottom: 1rem;
  text-align: center;
}

.col-md-6 {
  margin-bottom: 2rem;
  border: 1px solid #ccc;
  border-radius: 8px;
}
</style>
