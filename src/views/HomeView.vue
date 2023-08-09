<script setup lang="ts">
import { ref } from 'vue'

const price = ref<number>(0)
const description = ref<string>('')
const groupType = ref<string>('')

function saveToStorage() {
  // e.preventDefault();
  //   Fetch array from local storage
  const Expenses: any = localStorage.getItem('myExpenses')

  // create UUID for expenses

  const newExpenses = {
    price: price.value,
    item: description.value,
    group: groupType.value,
    created_at: new Date()
  }

  // An Error Might Occur Here Because i'm Trying to parse a null value

  const parsedExpenses = Expenses ? JSON.parse(Expenses) : []

  const ExpensesToSave = [...parsedExpenses, newExpenses]

  localStorage.setItem('myExpenses', JSON.stringify(ExpensesToSave))

  // store.appendToExpense(ExpensesToSave);

  price.value = 0
  description.value = ''
  groupType.value = ''
}
</script>

<template>
  <main>
    <div class="m-4">
      <form class="flex flex-col gap-4 justify-center items-center">
        <!-- Parent div -->
        <div class="flex flex-row gap-3">
          <!-- Description -->

          <div>
            <label for="description" class="block mb-2 text-sm font-medium text-white"
              >Description</label
            >
            <input
              type="text"
              id="description"
              class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg block w-full p-2.5"
              v-model="description"
              placeholder="what did you eat ?"
              required
            />
          </div>

          <!-- Price -->

          <div>
            <label for="price" class="block mb-2 text-sm font-medium text-white">Price</label>
            <input
              type="text"
              id="price"
              class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg block w-full p-2.5"
              v-model="price"
              placeholder="price"
              required
            />
          </div>
        </div>

        <select
          v-model="groupType"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg block p-2.5 mt-5 w-1/2"
        >
          <option disabled value="">Please Select</option>
          <option>Morning</option>
          <option>Night</option>
          <option>Misc</option>
        </select>

        <button
          class="bg-[#464bd8] hover:bg-[#4d46d9] focus:outline-none focus:ring-2 focus:ring-[#464bd8] focus:ring-opacity-50 py-2 px-4 font-mono rounded"
          @click="saveToStorage"
        >
          Add To Records
        </button>
      </form>

      <!-- Ability to preview -->
      <div class="container mx-auto bg-gray-200 rounded-xl shadow border p-8 m-10">
        <p class="text-black">What did you eat ? : {{ description }}</p>
        <p class="text-black">Price : {{ price }}</p>
        <span class="text-black">Type of Expense: {{ groupType }}</span>
      </div>
      <!-- style="padding: 3%" -->
    </div>
  </main>
</template>
