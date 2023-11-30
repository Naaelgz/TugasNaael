<script setup lang="ts">
  import { useRouter } from 'vue-router';
  import { useAuthStore } from '../stores/auth'
  import { ref } from 'vue'
  import axios from 'axios'
  import Swal from 'sweetalert2'

  const auth = useAuthStore()
  const username = ref('')
  const password = ref('')
  const router = useRouter()

  const handleLogin = async () => {
    const response = await axios({
      method: "post",
      url: "http://localhost:3000/login",
      data: {
        username: username.value,
        password: password.value
      }
    })

    if (response.data.status === "success") {
      Swal.fire({
        title: 'Success!',
        text: 'Welcome!',
        icon: 'success',
        confirmButtonText: 'Cool'
      })
      auth.login(username.value)
      router.push("/")
    }

    if (response.data.status === "error, username not found") {
      Swal.fire({
        title: 'Error!',
        text: 'Incorrect username!',
        icon: 'error',
        confirmButtonText: 'Try Again'
      })
    }

    if (response.data.status === "error, wrong password") {
      Swal.fire({
        title: 'Error!',
        text: 'Incorrect password!',
        icon: 'error',
        confirmButtonText: 'Try Again'
      })
    }
    console.log(response)
  }
</script>

<template>
  <div class="mt-20 sm:mx-auto sm:w-full sm:max-w-md bg-white rounded-md py-8 px-6">
    <h1 class="mb-5 text-[20px] text-center">Login</h1>
      <label for="username" class="block mb-2 text-sm font-medium text-gray-700">Username</label>
      <input v-model="username" id="Username" name="Username" type="text" class="w-full mb-5 border border-gray-300 rounded-lg px-3 py-2 focus:outline-none focus:border-[#4741b8]" autocomplete="off" required />
       <label for="username" class="block mb-2 text-sm font-medium text-gray-700">Password</label>
      <input v-model="password" id="Password" name="Password" type="password" class="w-full mb-5 border border-gray-300 rounded-lg px-3 py-2 focus:outline-none focus:border-[#4741b8]" autocomplete="off" required />
      <button @click="handleLogin()" class="w-full bg-[#0004ff] p-2 font-outfit text-white text-[16px] rounded-lg">Login</button>
  </div>
</template>