<template>

  <div>
    <h1>Log in</h1>
    <form @submit.prevent="login">
      <div>
        <label for="email">Email</label>
        <input type="email" id="email" v-model="Email" />
      </div>
      <div>
        <label for="password">Password</label>
        <input type="password" id="password" v-model="Password" />
      </div>
      <button type="submit">Log in</button>
    </form>
  </div>
</template>

<script setup>

import { ref } from 'vue'
import { useRouter } from 'vue-router'

const Email = ref('')
const Password = ref('')
const router = useRouter()

const login = async () => {
  const credentials = {
    email: Email.value,
    password: Password.value
  }
  const response = await fetch('http://localhost:3000/user/login', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(credentials)
  })

  const data = await response.json()
console.log(data);
localStorage.setItem('token', data.user.token)
  router.push('/')
}

</script>

<style scoped></style>
