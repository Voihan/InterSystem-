<!--
 * Component for displaying a list of leads.
 * 
 * @component LeadsList
 * @description
 * - Displays a list of leads, filtered and sorted by specified parameters.
 * - Includes the `SearchBar`, `SortControls` and `LeadItem` components.
 * - Implements the logic of pagination, sorting and filtering the list.
 * - The search is performed only when the button in the `SearchBar` component is clicked.
 * 
 * @props
 * - `contacts` (Array): An array of leads passed from the parent.
 *
 * @data
 * - `currentPage` (Number): Current page.
 * - `itemsPerPage` (Number): Number of leads on one page.
 * - `appliedQuery` (String): The applied search string is updated when the search button is pressed.
 * - `sortBy` (String): Current sort method.
 * 
 * @methods
 * - `updateSort(value)`: Updates the sort method.
 * - `nextPage()`: Go to next page.
 * - `prevPage()`: Go to previous page.
 * - `handleSearch(query)`: Updates the `appliedQuery` search string when a button in the `SearchBar` is clicked.
 * 
 * @computed
 * - `sortedAndFilteredLeads`: Returns a filtered and sorted array of leads.
 * - `totalPages` (Number): Total number of pages.
 * - `paginatedLeads` (Array): Leads displayed on the current page.
  -->

<template>
  <div>
    <!-- Header, which contains an input field, a search button filtered according to
         data from leads input, sort button (Opens a selection of sorting options) -->
    <header class="flex m-4 justify-center space-x-2">
      <!--Input component and search button -->
      <SearchBar @search="handleSearch" />
      <!-- Select component and sort buttons -->
      <SortControls @update:sort="updateSort" />
    </header>

    <!-- Main block where the list of leads is displayed -->
    <div class="container mx-auto p-4 sm:block">
      
      <!-- Wrapper for header and page navigation -->
      <div class="flex flex-col items-center my-8 md:flex-row md:justify-between md:items-center md:my-8">
        <!-- Page title -->
        <h1 class="text-2xl font-bold mb-4 md:mb-0">Lista potencjalnych klientów</h1>
      
        <!-- Page navigation -->
        <div class="flex items-center space-x-4">
          <!-- Current page from the total -->
          <h3 class="text-gray-600">Strona:</h3>
          <!-- Back button -->
          <button
            @click="prevPage"
            :disabled="currentPage === 1"
            class="bg-green-500 text-white p-2 rounded-full hover:bg-green-600 focus:outline-none disabled:opacity-50 disabled:cursor-not-allowed"
          >
            <!-- Left arrow icon -->
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-4 h-4">
              <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" />
            </svg>
          </button>
        
          <span class="text-gray-600 font-medium">
            {{ currentPage }} z {{ totalPages }}
          </span>
        
          <!-- "Forward" button -->
          <button
            @click="nextPage"
            :disabled="currentPage === totalPages"
            class="bg-green-500 text-white p-2 rounded-full hover:bg-green-600 focus:outline-none disabled:opacity-50 disabled:cursor-not-allowed"
          >
            <!-- Right arrow icon -->
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-4 h-4">
              <path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" />
            </svg>
          </button>
        </div>
      </div>

    <!-- We make the list of leads dynamic, display the filtered list on one page,
           if the number of leads is more than 0 -->
      <div v-if="sortedAndFilteredLeads.length > 0">
        <LeadItem
          v-for="lead in paginatedLeads"
          :key="lead.id"
          :lead="lead"
        />
      </div>
      <!-- Display a message if the number of leads from the list is 0 -->
      <div v-else>
        <p class="text-gray-500">Lista jest pusta</p>
      </div>
    </div>
  </div>
</template>

<script setup>
// Basic Vue methods for reactivity and calculations
import { ref, computed } from 'vue';

// Import components
// Input and search button
import SearchBar from './SearchBar.vue';
// Sort button and sorting options
import SortControls from './SortControls.vue';
// Component describing the box of one lead
import LeadItem from './LeadItem.vue';

// Accept the "contacts" prop from the parent with a static list of leads
const props = defineProps({
  contacts: {
    type: Array, 
    required: true, 
  },
});

//Declare Vue Variables

// Reactive variable for search string
const appliedQuery = ref(''); // Applied filtering query

const handleSearch = (query) => {
  appliedQuery.value = query; // Apply the search string when the button is pressed
};
// Reactive variable for the selected sort method
const sortBy = ref('');
// Reactive variables for pagination
const currentPage = ref(1); // Current page
const itemsPerPage = ref(10); // Number of elements per page

// Functions

// Function to update the value of the sorting method
const updateSort = (value) => {
  sortBy.value = value;
};


// Function that calculates the total number of pages
const totalPages = computed(() => {
  return Math.ceil(sortedAndFilteredLeads.value.length / itemsPerPage.value);
});

// Leads to display on the current page
const paginatedLeads = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage.value;
  const end = start + itemsPerPage.value;
  return sortedAndFilteredLeads.value.slice(start, end);
});

// Methods for switching pages
const nextPage = () => {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
  }
};

const prevPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
  }
};

// Calculated property for filtering and sorting the list of leads
// Filtering is performed based on data from the search string (searchQuery),
// including first name, last name and email of each lead. The value is updated dynamically
// when the search string changes.
const sortedAndFilteredLeads = computed(() => {  
  const filtered = props.contacts.filter((lead) => {
    const leadData = `${lead.name || ''} ${lead.last_name || ''} ${lead.email || ''}`;
    return leadData.toLowerCase().includes(appliedQuery.value.toLowerCase());
  });

  const sorted = [...filtered];
// Sorting
// Sorts the filtered list of leads based on the selected sortBy criterion
// Supported criteria:
// - 'date': Sorts by send date in descending order (newest above oldest).
// - 'alphabet': Sorts by lead name in alphabetical order (ascending).
// - 'websiteId': Sorts by website ID in ascending order (numeric comparison).
// - 'region': Sorts by region in alphabetical order (ascending).
// - 'hasMessage': Sorts by presence and length of messages (leads with longer messages above).
// If the sort criterion is not specified or not recognized, the original filtered list is returned.
switch (sortBy.value) {
    case 'date':
      
      return sorted.sort((a, b) => {
        const dateA = a.sent ? new Date(a.sent.split('.').reverse().join('-')) : new Date(0);
        const dateB = b.sent ? new Date(b.sent.split('.').reverse().join('-')) : new Date(0);
        return dateB - dateA;
    });
    case 'alphabet':
      return sorted.sort((a, b) => (a.name || '').localeCompare(b.name || ''));
    case 'websiteId':
      return sorted.sort((a, b) => Number(a.website_id) - Number(b.website_id));
    case 'region':
      return sorted.sort((a, b) => (a.region || '').localeCompare(b.region || ''));
    case 'hasMessage':
      return sorted.sort((a, b) => (b.message?.length || 0) - (a.message?.length || 0));
    default:
      return sorted;
  }
});



</script>
