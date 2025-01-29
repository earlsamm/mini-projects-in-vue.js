<script setup>
import { ref, onMounted } from 'vue'

let formData = ref({
  name: '',
  email: '',
  password: '',
  confirmPassword: '',
})

let errors = ref({
  name: '',
  email: '',
  password: '',
  confirmPassword: '',
})

let validate = () => {
  let isValid = true

  if (!formData.value.name || formData.value.name === '' || formData.value.name === null) {
    errors.value.name = 'Name is required'
    isValid = false
  } else {
    errors.value.name = ''
  }

  if (formData.value.name < 3) {
    errors.value.name = 'Name too short'
    isValid = false
  }

  if (formData.value.name > 20) {
    errors.value.name = 'Name cannot be more than 20 characters'
    isValid = false
  }

  if (!formData.value.email) {
    errors.value.email = 'Email is required'
    isValid = false
  } else {
    errors.value.email = ''
  }

  if (!formData.value.password) {
    errors.value.password = 'Password is required'
    isValid = false
  } else {
    errors.value.password = ''
  }

  if (formData.value.password !== formData.value.confirmPassword) {
    errors.value.confirmPassword = 'Passwords do not match'
    isValid = false
  } else {
    errors.value.confirmPassword = ''
  }

  return isValid
}

onMounted(() => {
  document.querySelector('#name').focus()
})

let onSubmit = () => {
  if (validate()) {
    alert('Form submitted successfully')
  }
}
</script>

<template>
  <div class="form">
    <div>
      <label for="name">Name:</label>
      <input v-model="formData.name" type="text" id="name" />
      <div class="error">{{ errors.name }}</div>
    </div>
    <div>
      <label for="email">Email:</label>
      <input v-model="formData.email" type="email" id="email" />
      <div class="error">{{ errors.email }}</div>
    </div>
    <div>
      <label for="password">Password:</label>
      <input v-model="formData.password" type="password" id="password" />
      <div class="error">{{ errors.password }}</div>
    </div>
    <div>
      <label for="confirmPassword">Confirm Password:</label>
      <input v-model="formData.confirmPassword" type="password" id="confirmPassword" />
      <div class="error">{{ errors.confirmPassword }}</div>
    </div>
    <button @click="onSubmit" class="submit">Submit</button>
  </div>
</template>

<style scoped>
.form {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

label {
  display: block;
  margin-bottom: 5px;
}

input {
  width: 100%;
  padding: 5px;
  margin-bottom: 10px;
}

button {
  padding: 5px 10px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

.error {
  color: red;
  margin-bottom: 10px;
}
</style>
