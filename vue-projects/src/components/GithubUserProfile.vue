<script setup>
import { ref, onMounted, watch } from 'vue'

const username = ref('')
const userProfile = ref(null)
const error = ref(null)

const fetchUserProfile = async () => {
  try {
    const response = await fetch(`https://api.github.com/users/${username.value}`)
    const data = await response.json()

    if (!response.ok) {
      error.value = 'User not found'
      userProfile.value = null
    } else {
      error.value = null
      userProfile.value = data
    }
  } catch (err) {
    console.error('Error fetching data: ' + err)
    error.value = 'An error occurred while fetching the user profile'
  }
}

onMounted(() => {
  document.getElementById('username').focus()
})

// Prevent the default behavior of the Enter key
window.addEventListener('keydown', (event) => {
  if (event.key === 'Enter') {
    event.preventDefault()
  }
})

// Handle the keydown event
window.addEventListener('keydown', (event) => {
  if (event.key === 'Enter') {
    fetchUserProfile()
  }
})

// Clear user profile when username is empty
watch(username, () => {
  if (username.value === '') {
    userProfile.value = null
  }
})
</script>
<template>
  <div class="github-user-profile">
    <input
      type="text"
      class="form-control"
      v-model="username"
      placeholder="Enter a GitHub username"
      id="username"
    />
    <div v-if="error" class="error">{{ error }}</div>
    <div v-else-if="userProfile" class="profile">
      <img :src="userProfile.avatar_url" alt="Avatar" class="user-img" />
      <h2>GitHub Profile for {{ userProfile.login }}</h2>
      <p>Name: {{ userProfile.name }}</p>
      <p>Location: {{ userProfile.location }}</p>
      <p>Bio: {{ userProfile.bio }}</p>
      <p>Followers: {{ userProfile.followers }}</p>
      <p>Following: {{ userProfile.following }}</p>
      <p>Public Repos: {{ userProfile.public_repos }}</p>

      <a :href="userProfile.html_url" target="_blank">View Profile</a>
    </div>
  </div>

  <div class="text-center">
    <button @click="fetchUserProfile" class="btn btn-primary" :disabled="username == ''">
      Fetch Profile
    </button>
  </div>
</template>
<style scoped>
.github-user-profile {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
}

.error {
  color: red;
  margin-bottom: 1rem;
}

.profile {
  text-align: center;
}

.user-img {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin: 0 auto;
  margin-bottom: 1rem;
}
</style>
