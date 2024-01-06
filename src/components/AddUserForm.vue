<template>
  <div>
    <h1>Add User</h1>
    <form @submit.prevent="addUser">
      <div>
        <label for="username">Username</label>
        <input type="text" id="username" v-model="username" />
      </div>
      <div>
        <label for="email">Email</label>
        <input type="email" id="email" v-model="email" />
      </div>
      <div>
        <label for="password">Password</label>
        <input type="password" id="password" v-model="password" />
      </div>
      <div>
        <label for="address">Address</label>
        <input type="text" id="address" v-model="address" />
      </div>
      <div>
        <label for="role">Role</label>
        <select name="role" id="role" v-model="role">
          <option value="admin">Admin</option>
          <option value="user">User</option>
        </select>
      </div>
      <div>
        <label for="status">Status</label>
        <select name="status" id="status" v-model="status">
          <option value="active">Active</option>
          <option value="inactive">Inactive</option>
        </select>
      </div>

      <button type="submit">Add User</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const username = ref('')
const email = ref('')
const password = ref('')
const address = ref('')
const role = ref('')
const status = ref('')
const router = useRouter()

const addUser = async () => {
  const credentials = {
    username: username.value,
    email: email.value,
    password: password.value,
    address: address.value,
    role: role.value,
    status: status.value
  }
  const response = await fetch( 'http://localhost:3000/user/add', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(credentials)
  })

  const data = await response.json()
  console.log(data)
  localStorage.setItem('token', data.newUser.token)

  router.push('/all')
}
</script>

<style scoped></style>
