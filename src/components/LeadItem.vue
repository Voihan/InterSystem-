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
  <div class="border-2 p-4 rounded-lg shadow mb-4">
    <!-- Main row -->
    <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between">
      <!-- Left side: Basic information -->
      <div class="sm:flex-1">
        <p class="text-lg font-semibold">{{ lead.name }} {{ lead.last_name }}</p>
        <p class="text-gray-600">Email: {{ lead.email }}</p>
        <p class="text-gray-600">Numer telefonu: {{ lead.phone }}</p>
      </div>

      <!-- Central part: Dropdown button -->
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

      <!-- Right side: Message -->
      <div class="sm:flex-1 border-t sm:border-t-0 sm:border-l sm:pl-4 pt-4 sm:pt-0">
        <div class="flex justify-between items-start">
          <!-- Title and date -->
          <h4 class="text-lg font-semibold text-right sm:text-left">Wiadomość:</h4>
          <span class="text-sm text-gray-500 text-right">{{ lead.sent }}</span>
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
    </div>

    <!-- Dropdown: Additional information -->
    <div v-if="isOpen" class="mt-4 bg-gray-50 p-3 rounded">
      <p><strong>Wojewódstwo:</strong> {{ lead.region }}</p>
      <p><strong>Website ID:</strong> {{ lead.website_id }}</p>
      <p><strong>Score:</strong> {{ lead.score }}</p>
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
