<script setup lang="ts">
import { ref, onMounted } from 'vue'
import axios from 'axios'
import { useRoute } from 'vue-router'
import type { Post } from '@/types'

let post = ref<Post>({id: 0, title: '', body: '' })
let loading = ref(true)
const route = useRoute()

async function getPost() {
    const response = await axios.get(`http://127.0.0.1:8000/blog/api/${route.params.id}/`)
    loading.value = false
    post.value = response.data
}

onMounted(async () => {
    await getPost()
})
</script>

<template>
    <main>
        <div v-if="loading">LOADING...</div>
        <div v-else>
            <h1 class="text-3xl">{{ post.title }}</h1>
            <p>{{ post.body }}</p>
        </div>
    </main>
</template>