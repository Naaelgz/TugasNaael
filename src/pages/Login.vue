<script setup lang="ts">
  import { useRouter } from 'vue-router';
  import { useAuthStore } from '../stores/auth'
  import { ref } from 'vue'

  const auth = useAuthStore()
  const username = ref('')
  const router = useRouter()

  const handleLogin = () => {
    auth.login(username.value)
    router.push('/')
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