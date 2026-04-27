<script setup>
import { ref, onMounted } from 'vue'

// tempat menyimpan data
const posts = ref([])

// status loading
const loading = ref(true)

// fungsi ambil data dari API
const fetchPosts = async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users')
    const data = await response.json()
    posts.value = data
  } catch (error) {
    console.log('Terjadi error:', error)
  } finally {
    loading.value = false
  }
}

// dijalankan saat halaman pertama kali dibuka
onMounted(() => {
  fetchPosts()
})
</script>

<template>
  <div class="min-h-screen flex flex-col items-center">
    <h1 class="text-3xl font-bold mb-6 mt-6">Data Posts</h1>

    <!-- loading -->
    <p v-if="loading">Loading...</p>

    <!-- data -->
    <ul v-else class="w-full max-w-md border">
      <li v-for="users in posts" :key="users.id">
        <a
          href="#"
          class="block p-6 border-b text-center"
        >
          <h5 class="text-xl font-semibold">
            {{ users.name }}
          </h5>
          <p class="text-gray-600">
            {{ users.email }}
          </p>
        </a>
      </li>
    </ul>
  </div>
</template>