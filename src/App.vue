<template>
  <PaginatedList v-slot="{ data }" :data="posts">
    <div class="flex flex-wrap justify-center gap-4 mt-10">
      <div v-for="item in data" :key="item.id" class="max-w-sm p-6 bg-white border border-neutral-200 rounded-lg shadow">
        <div class="">
          <h5 class="mb-2 text-2xl font-bold tracking-tight text-neutral-900">{{ item.title }} </h5>
          <p class="mb-3 font-normal text-neutral-600">{{ item.body }}</p>
        </div>
        <a href="#" class="inline-flex items-center px-3 py-2 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300">
          Read more
          <svg aria-hidden="true" class="w-4 h-4 ml-2 -mr-1" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
        </a>
      </div>
    </div>
  </PaginatedList>
</template>

<script setup>
import { ref } from 'vue'
import PaginatedList from '@/components/PaginatedList.vue'

const posts = ref([])

fetch('https://jsonplaceholder.typicode.com/posts')
  .then(response => response.json())
  .then(p => posts.value = p)
</script>
