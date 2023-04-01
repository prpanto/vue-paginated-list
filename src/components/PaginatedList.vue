<template>
  <slot :data="paginatedData"/>

  <nav class="py-10 flex justify-center items-center">
    <ul class="inline-flex items-center -space-x-px">
      <li>
        <button :disabled="pageNumber === 0" @click="prev()" class="block px-3 py-2 ml-0 leading-tight text-neutral-500 bg-white border border-neutral-300 rounded-l-lg hover:bg-neutral-100 hover:text-neutral-700">
          <svg aria-hidden="true" class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z" clip-rule="evenodd"></path></svg>
        </button>
      </li>
      <li v-for="count in pageCount" :key="count">
        <button v-if="(pageNumber + 1) === count" class="z-10 px-3 py-2 leading-tight text-blue-600 border border-blue-300 bg-blue-50 hover:bg-blue-100 hover:text-blue-700" @click="setPage(count)">
          {{ count }}            
        </button>

        <button v-else class="px-3 py-2 leading-tight text-neutral-500 bg-white border border-neutral-300 hover:bg-neutral-100 hover:text-neutral-700" @click="setPage(count)">
          {{ count }}            
        </button>
      </li>
      <li>
        <button :disabled="pageNumber >= pageCount -1" @click="next()" class="block px-3 py-2 leading-tight text-neutral-500 bg-white border border-neutral-300 rounded-r-lg hover:bg-neutral-100 hover:text-neutral-700">
          <svg aria-hidden="true" class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd"></path></svg>
        </button>
      </li>
    </ul>
  </nav>
</template>

<script setup>
import { computed, ref } from 'vue'

const props = defineProps({
  data: {
    type: Array,
    required: true
  }
})

const pageNumber = ref(0)
const size = ref(8)

const start = computed(() => pageNumber.value * size.value)
const end = computed(() => start.value + size.value)
const pageCount = computed(() => Math.ceil(props.data.length / size.value))
const paginatedData = computed(() => props.data.slice(start.value, end.value))

const next = () => pageNumber.value++
const prev = () => pageNumber.value--
const setPage = (page) => pageNumber.value = (page - 1)
</script>
