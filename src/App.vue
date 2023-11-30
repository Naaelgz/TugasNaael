<script setup lang="ts">
  import { useRouter } from 'vue-router';
  import { RouterLink, RouterView } from 'vue-router'
  import { useAuthStore } from './stores/auth';

  const auth = useAuthStore()
  const router = useRouter()

  const handleLogout = () => {
    auth.logout()
    router.push('/login')
  }

  const warn = () => {
    alert("You have to login")
  }
</script>

<template>
  <div class="w-full h-[100vh] bg-gray-100">
      <!-- Navbar -->
    <div class="w-full flex p-4 align-middle justify-between items-center bg-[#1A1A1A] font-mono font-[400] text-[18px] text-[#E1E1E1] ">
      <div class="flex space-x-5">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink v-if="auth.username" to="/restricted">Restricted Page</RouterLink>
        <p v-else @click="warn()">Restricted Page</p>
      </div>
      <div class="flex space-x-5 items-center">
        <p v-if="auth.username" class="text-[#ffffff]">Welcome, {{ auth.username }}</p>
        <div v-if="auth.username">
          <button to="/login" class="bg-[#0004ff] p-2 text-[16px] rounded-md" @click="handleLogout()">Logout</button>
        </div>
        <div v-else>
          <RouterLink to="/login" class="bg-[#0004ff] p-2 text-[16px] rounded-md">Login</RouterLink>
        </div>
      </div>
    </div>
    <RouterView />
  </div>
</template>

