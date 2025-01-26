<!--
* Component for managing sorting of the list of leads.
*
* @component SortControls
* @description
* - Contains a button for displaying a drop-down list with sorting options.
* - Allows you to select a sorting method.
*
* @emits
* - `update:sort` (String): Passes the selected sorting method to the parent.
*
* @methods
* - `toggleDropdown()`: Opens or closes the drop-down list.
* - `selectSortOption(value)`: Passes the selected sorting value and closes the drop-down list.
-->


<template>
    <div class="relative">
<!-- Sorting button with "horizontal stripes" icon when pressed, "toggleDropdown" is performed and a selection of sorting options is opened-->
      <button
        @click="toggleDropdown"
        class="bg-green-500 text-white p-2 rounded-full hover:bg-green-600 focus:outline-none"
      >
      <!-- Icon for "horizontal stripes" sorting options -->
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
            d="M4 6h16M4 12h8m-8 6h16"
          />
        </svg>
      </button>
  
<!-- Dropdown list -->
<!-- Conditional rendering: only displays the list if 'isDropdownOpen' is true -->
      <div
        v-if="isDropdownOpen"
        class="absolute top-12 right-0 bg-white border-2 rounded-lg shadow-lg z-10 w-40"
      >

      <!-- Text before sorting options -->
      <div class="bg-green-500 px-4 py-2 text-sm font-semibold text-white border-b">
      Sortuj według:
      </div>
      <!-- List with sorting options -->
        <ul>
            <!-- Loop to render each option from the 'sortOptions' array -->
            <!-- Unique key for each option -->
            <!-- Click handler: calls the 'selectSortOption' method with the selected value -->
          <li
            v-for="option in sortOptions"
            :key="option.value"
            @click="selectSortOption(option.value)"
            class="px-4 py-2 hover:bg-gray-100 cursor-pointer"
          >
          <!-- Display text label for option -->
            {{ option.label }}
          </li>
        </ul>
      </div>
    </div>
  </template>
  
  <script setup>
  // Vue's core methods for reactivity and computation
  import { ref } from 'vue';
  
  // State of the dropdown list
  const isDropdownOpen = ref(false);
  
  // List of sorting options
  const sortOptions = [
    { value: 'date', label: 'Data' },
    { value: 'alphabet', label: 'Alfabet' },
    { value: 'websiteId', label: 'Website ID' },
    { value: 'region', label: 'Wojewódstwo' },
    { value: 'hasMessage', label: 'Zostawiona wiadomośc' },
  ];
  
  // Emitter to pass the selected value to the parent
  const emit = defineEmits(['update:sort']);
  
  // Function to switch the state of the drop-down list
  const toggleDropdown = () => {
    isDropdownOpen.value = !isDropdownOpen.value;
  };
  
  // Function for selecting sorting option
  const selectSortOption = (value) => {
    emit('update:sort', value);
    isDropdownOpen.value = false; // Close the dropdown list
  };
  </script>
  <style></style>
  