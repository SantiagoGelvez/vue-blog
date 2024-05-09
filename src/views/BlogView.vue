<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { ref, onMounted } from 'vue'
import axios from 'axios'
import type { Post } from '@/types';

let postList = ref<Post[]>([])
let loading = ref(true)

async function getPosts() {
    const response = await axios.get('http://127.0.0.1:8000/blog/api/')
    loading.value = false
    postList.value = response.data
}

onMounted(async () => {
    await getPosts()
})
</script>

<template>
    <main>
        <h1 class="text-3xl">Blog List</h1>
        <br>
        <div v-if="loading">
            <h1>LOADING...</h1>
        </div>

        <ul v-else>
            <li v-for="post in postList">
                <RouterLink :to="{ name: 'blog-post', params: { id: post.id } }">
                    <h2 class="text-xl">{{ post.title }}</h2>
                </RouterLink>
                <h2 class="text-xl truncate">{{ post.title }}</h2>
                <p>{{ post.body }}</p>
                <br><hr><br>
            </li>
        </ul>
    </main>
</template>

<style scoped></style>