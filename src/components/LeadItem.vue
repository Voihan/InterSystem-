<!-- 
 * Component for displaying information about one lead.
 * 
 * @component LeadItem
 * @description
 * - Displays basic information about the lead: first name, last name, email, message, region and date.
 * - Contains buttons to expand details and open a modal window.
 * 
 * @props
 * - `lead` (Object): An object with data about a specific lead.
 * 
 * @methods
 * - `toggleDetails()`: Controls the disclosure status of additional data.
 * - `openModal()`: Opens a modal window with the full text of the message.
 * - `closeModal()`: Closes the modal window.
 * 
 * @computed
 * - `isTruncated`: Determines whether the message should be shortened.
 * - `truncatedMessage`: Returns a shortened message.
  -->

<template>
  <!-- Main box of one lead -->
  <div class="border-2 bg-white p-4 rounded-lg shadow mb-4 ">
    <!-- Main row -->
    <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between">
      <!-- Left side: Basic information -->
      <div class="sm:flex-1">
        <div class="flex items-center">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-6 text-green-500 mr-4">
            <path fill-rule="evenodd" d="M18.685 19.097A9.723 9.723 0 0 0 21.75 12c0-5.385-4.365-9.75-9.75-9.75S2.25 6.615 2.25 12a9.723 9.723 0 0 0 3.065 7.097A9.716 9.716 0 0 0 12 21.75a9.716 9.716 0 0 0 6.685-2.653Zm-12.54-1.285A7.486 7.486 0 0 1 12 15a7.486 7.486 0 0 1 5.855 2.812A8.224 8.224 0 0 1 12 20.25a8.224 8.224 0 0 1-5.855-2.438ZM15.75 9a3.75 3.75 0 1 1-7.5 0 3.75 3.75 0 0 1 7.5 0Z" clip-rule="evenodd" />
          </svg>
          <p class="text-lg font-semibold">{{ lead.name }} {{ lead.last_name }}</p>
        </div>

        <div class="flex items-center">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-6 text-green-500 mr-4 mt-2">
            <path d="M1.5 8.67v8.58a3 3 0 0 0 3 3h15a3 3 0 0 0 3-3V8.67l-8.928 5.493a3 3 0 0 1-3.144 0L1.5 8.67Z" />
            <path d="M22.5 6.908V6.75a3 3 0 0 0-3-3h-15a3 3 0 0 0-3 3v.158l9.714 5.978a1.5 1.5 0 0 0 1.572 0L22.5 6.908Z" />
          </svg>
          <p class="text-gray-600">Email: {{ lead.email }}</p>

        </div>
        
        <div class="flex items-center">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-6 text-green-500 mr-4 mt-2">
            <path fill-rule="evenodd" d="M1.5 4.5a3 3 0 0 1 3-3h1.372c.86 0 1.61.586 1.819 1.42l1.105 4.423a1.875 1.875 0 0 1-.694 1.955l-1.293.97c-.135.101-.164.249-.126.352a11.285 11.285 0 0 0 6.697 6.697c.103.038.25.009.352-.126l.97-1.293a1.875 1.875 0 0 1 1.955-.694l4.423 1.105c.834.209 1.42.959 1.42 1.82V19.5a3 3 0 0 1-3 3h-2.25C8.552 22.5 1.5 15.448 1.5 6.75V4.5Z" clip-rule="evenodd" />
          </svg>
  
          <p class="text-gray-600">Numer telefonu: {{ lead.phone }}</p>
          
        </div>
        <div class="flex  items-center">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-6 text-green-500 mr-4 mt-2">
            <path d="M12.75 12.75a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0ZM7.5 15.75a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5ZM8.25 17.25a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0ZM9.75 15.75a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5ZM10.5 17.25a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0ZM12 15.75a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5ZM12.75 17.25a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0ZM14.25 15.75a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5ZM15 17.25a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0ZM16.5 15.75a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5ZM15 12.75a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0ZM16.5 13.5a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5Z" />
            <path fill-rule="evenodd" d="M6.75 2.25A.75.75 0 0 1 7.5 3v1.5h9V3A.75.75 0 0 1 18 3v1.5h.75a3 3 0 0 1 3 3v11.25a3 3 0 0 1-3 3H5.25a3 3 0 0 1-3-3V7.5a3 3 0 0 1 3-3H6V3a.75.75 0 0 1 .75-.75Zm13.5 9a1.5 1.5 0 0 0-1.5-1.5H5.25a1.5 1.5 0 0 0-1.5 1.5v7.5a1.5 1.5 0 0 0 1.5 1.5h13.5a1.5 1.5 0 0 0 1.5-1.5v-7.5Z" clip-rule="evenodd" />
          </svg>
          <span class="text-sm text-gray-500 text-right">{{ lead.sent }}</span>
        </div>
      </div>

      
      <!-- Central part: Message -->
      <div class="sm:flex-1 border-x-2 border-green-500 sm:border-x sm:pl-4 p-4 sm:pt-0 m-4">
        <div class="flex justify-between items-start">
          <!-- Title and date -->
          <h4 class="text-lg font-semibold text-right sm:text-left">Wiadomość:</h4>
          
        </div>
        <!-- Message text with green dots -->
        <p class="text-gray-800 mt-2 text-justify sm:text-left">
          {{ truncatedMessage }}
          <span
          v-if="isTruncated"
          @click="openModal"
          class="text-lg font-bold text-green-500 cursor-pointer hover:underline"
          >
          ...
        </span>
      </p>
    </div>
        <!-- Right side : Dropdown button -->
        <!-- The dropdown button shows additional information according to the API -->
        <div class="my-4 sm:my-0 sm:mx-4 flex justify-center">
          <button
            @click="toggleDetails"
            :class="isOpen ? 'rotate-180' : ''"
            class="bg-green-500 text-white p-3 rounded-full shadow hover:bg-green-600 transition-transform duration-300 focus:outline-none"
          >
          <!-- Button icon -->
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="2"
              stroke="currentColor"
              class="w-5 h-5"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M19 9l-7 7-7-7"
              />
            </svg>
          </button>
        </div>
    </div>

    <!-- Dropdown: Additional information -->
    <div v-if="isOpen" class="mt-4 bg-green-500 p-3 rounded">
      <p class="text-white"><strong>Województwo:</strong> {{ lead.region }}</p>
      <p class="text-white"><strong>Website ID:</strong> {{ lead.website_id }}</p>
      <p class="text-white"><strong>Score:</strong> {{ lead.score }}</p>
    </div>

    <!-- Modal window with the full text of the message -->
    <div
      v-if="isModalOpen"
      class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center z-50"
    >
  <div class="bg-white p-6 rounded shadow-lg max-w-lg w-full">
    <h2 class="text-xl font-bold mb-4">Wiadomość</h2>
    <!-- Message text with automatic line breaks -->
    <p class="text-gray-800 break-words overflow-y-auto max-h-64">
      {{ lead.message || 'Nie ma wiadomości' }}
    </p>
    <!-- Button to close the modal window that appears -->
    <div class="flex justify-end mt-4">
      <button
        @click="closeModal"
        class="bg-green-500 text-white p-3 rounded-full shadow hover:bg-green-600 focus:outline-none"
      >
      <!-- Close button icon -->
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="2"
          stroke="currentColor"
          class="w-5 h-5"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M6 18L18 6M6 6l12 12"
          />
        </svg>
      </button>
    </div>
  </div>
</div>
  </div>
</template>

<script setup>
// Basic Vue methods for reactivity and calculations
import { ref, computed } from 'vue';

// Props for transmitting lead data
const props = defineProps({
  lead: {
    type: Object,
    required: true,
  },
});

// Manage dropdown and modal window state
const isOpen = ref(false);
const isModalOpen = ref(false);

// Maximum message text length to display
const maxMessageLength = 170;

// Computed property to shorten text
const isTruncated = computed(() => props.lead.message && props.lead.message.length > maxMessageLength);
const truncatedMessage = computed(() =>
  isTruncated.value ? props.lead.message.slice(0, maxMessageLength) : props.lead.message
);

// Methods for opening/closing a modal window
const openModal = () => {
  isModalOpen.value = true;
};

const closeModal = () => {
  isModalOpen.value = false;
};

// Method for controlling dropdown
const toggleDetails = () => {
  isOpen.value = !isOpen.value;
};
</script>

<style scoped>
/* Button animation */
button {
  transition: transform 0.3s ease;
}
button.rotate-180 {
  transform: rotate(180deg);
}

/* Modal window dimming style */
.fixed {
  background: rgba(0, 0, 0, 0.5);
}


</style>
