<script setup lang="ts">
import { onMounted, ref } from 'vue'
// import { store } from "../app/store";
import moment from 'moment'

interface Iexpense {
  price: number
  item: string
  group: string
  created_at: string
}

const AllExpenses = ref<Iexpense[]>([
  {
    price: 100,
    item: 'Bread and Bama',
    group: 'Night',
    created_at: ''
  }
])

function fetchList() {
  const Expenses = localStorage.getItem('myExpenses')

  // Check if Expenses is null, and if so, set it to an empty array
  const parsedExpenses = Expenses ? JSON.parse(Expenses) : []

  console.log(parsedExpenses)
  // fetch from local storage and set to store
  AllExpenses.value = parsedExpenses
}

onMounted(() => {
  console.log(`the component is now mounted.`)
  fetchList()
})
</script>

<template>
  <div class="relative overflow-x-auto mt-4">
    <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
      <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
        <tr>
          <th scope="col" class="px-6 py-3">Name</th>
          <th scope="col" class="px-6 py-3">Price</th>
          <th scope="col" class="px-6 py-3">Group</th>
          <th scope="col" class="px-6 py-3">Date</th>
        </tr>
      </thead>
      <tbody>
        <!-- Loop through all Expenses -->
        <tr v-for="({ price, item, group, created_at }, index) in AllExpenses" :key="index">
          <th
            scope="row"
            class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
          >
            {{ item }}
          </th>
          <td class="px-6 py-4">{{ price }}</td>
          <td class="px-6 py-4">{{ group }}</td>
          <td class="px-6 py-4">
            {{ created_at ? moment(created_at).format('DD-MMM-YYYY') : '--' }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style></style>
