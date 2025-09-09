<script setup>
import { ref, onMounted } from "vue"
import axios from "../axios"

const user = ref(null)
const errorMessage = ref("")

onMounted(async () => {
  try {
    const response = await axios.get("/user", {
      headers: {
        Authorization: `Bearer ${localStorage.getItem("token")}`
      }
    })
    user.value = response.data
  } catch (error) {
    errorMessage.value = "No autorizado, vuelve a iniciar sesión"
    window.location.href = "/login"
  }
})

const logout = () => {
  localStorage.removeItem("token")
  window.location.href = "/login"
}
</script>

<template>
  <div class="p-8">
    <h1 class="text-2xl font-bold mb-4">Dashboard</h1>
    <p v-if="user">Bienvenido, {{ user.name }} ({{ user.email }})</p>
    <p v-if="errorMessage" class="text-red-600">{{ errorMessage }}</p>

    <button
      @click="logout"
      class="mt-4 bg-red-600 text-white px-4 py-2 rounded hover:bg-red-700"
    >
      Cerrar sesión
    </button>
  </div>
</template>