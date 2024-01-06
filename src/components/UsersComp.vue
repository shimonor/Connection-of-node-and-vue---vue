<template>
  <div>
    <h1>Users</h1>

    <div v-for="user in users" :key="user.id">
    <h2>  {{ user.username }}</h2>
      <p> {{ user.email }}</p>
      <h2>  {{ user.address }}</h2> 
      <p> {{ user.role }}</p>
      <p> {{ user.status }}</p>
      <button @click="deleteUser(user.id)">Delete</button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
const users = ref([])

onMounted(() => {
  getUsers()
})

const getUsers = async () => {
  const response = await fetch('http://localhost:3000/user', {
    headers: {
      Authorization: `Bearer ${localStorage.getItem('token')}`
    }
  })

  const data = await response.json()
  users.value = data.users
}

const deleteUser = async (id) => {
  const response = await fetch(`http://localhost:3000/user/${id}`, {
    method: 'DELETE',
    headers: {
      Authorization: "Bearer " + localStorage.getItem('token')
    }
  })

  await response.json()
  getUsers()
}
</script>

<style scoped></style>
