<script setup>
import { ref } from "vue"
import { useRouter } from 'vue-router'
import axios from "../axios"

const router = useRouter()
const email = ref("")
const password = ref("")
const errorMessage = ref("")

const handleLogin = async () => {
  try {
    const response = await axios.post("/login", {
      email: email.value,
      password: password.value
    })

    // Guardar token primero
    localStorage.setItem("token", response.data.access_token)

    // Redirigir al dashboard usando Vue Router (SPA)
    router.push('/dashboard')

    // Opcional: obtener info del usuario
    const userResponse = await axios.get("/user", {
      headers: {
        Authorization: `Bearer ${localStorage.getItem("token")}`
      }
    })
    console.log(userResponse.data)

  } catch (error) {
    errorMessage.value = error.response?.data?.message || "Error en el login"
  }
}
</script>


<template>
  <div class="flex items-center justify-center min-h-screen bg-gray-100">
    <div class="bg-white shadow-2xl rounded-2xl p-8 w-full max-w-md">
      <h2 class="text-2xl font-bold text-center mb-6">Iniciar Sesión</h2>

      <form @submit.prevent="handleLogin" class="space-y-4">
        <div>
          <label for="email" class="block text-sm font-medium text-gray-700">Correo</label>
          <input
            v-model="email"
            type="email"
            id="email"
            required
            class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-xl shadow-sm focus:ring-blue-500 focus:border-blue-500"
          />
        </div>

        <div>
          <label for="password" class="block text-sm font-medium text-gray-700">Contraseña</label>
          <input
            v-model="password"
            type="password"
            id="password"
            required
            class="mt-1 block w-full px-4 py-2 border border-gray-300 rounded-xl shadow-sm focus:ring-blue-500 focus:border-blue-500"
          />
        </div>

        <button
          type="submit"
          class="w-full bg-blue-600 text-white py-2 px-4 rounded-xl hover:bg-blue-700 transition"
        >
          Entrar
        </button>
      </form>

      <p v-if="errorMessage" class="mt-4 text-red-600 text-sm text-center">
        {{ errorMessage }}
      </p>
    </div>
  </div>
</template>
