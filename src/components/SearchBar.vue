<!--
* Component for searching through a list of leads.
*
* @component SearchBar
* @description
* - Provides an input field and button for searching.
* - Emit events to update the search bar and perform the search.
*
* @emits
* - `search` (String): Passes the text of the search bar when the search button is clicked.
* @data
* - `query` (String): Local search string used for entering text.
*
* @methods
* - `handleSearch()`: Emit the `search` event and pass the current search bar to the parent component.
-->


<template>
<!-- We describe a dynamic field for entering data for searching and filtering the entire list of leads -->
    <div class="flex space-x-2">
      <!-- Search input field -->
      <!-- Two-way data binding: binds the field value to the 'query' variable -->
      <!-- Placeholder text, displays "Search" while field is empty -->
       <input
        type="text"
        v-model="query"
        class="w-full border border-gray-300 rounded-sm p-2 focus:outline-none focus:ring focus:ring-green-300"
        placeholder="Search"
      />
      <!-- Search button with magnifying glass icon, when pressed "handleSearch" is performed -->
      <button
        @click="handleSearch"
        class="bg-green-500 text-white p-2 rounded-full hover:bg-green-600 focus:outline-none"
      >
      <!-- Magnifying glass icon -->
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="2"
          stroke="currentColor"
          class="w-6 h-6"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M21 21l-4.35-4.35m1.2-5.4a7.5 7.5 0 11-15 0 7.5 7.5 0 0115 0z"
          />
        </svg>
      </button>
    </div>
  </template>
  
  <script setup>
  // Vue's core methods for reactivity and computation
  import { ref } from 'vue';

  // Define the 'update:searchQuery' event
  const emit = defineEmits(['update:searchQuery', 'search']);
  // Declare the variable "query"
  const query = ref('');
  
  
  const handleSearch = () => {
  emit('search', query.value); // Pass the search string to the parent
  };
  </script>
  