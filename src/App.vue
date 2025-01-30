 <!-- 
 * The main component of the application.
 * 
 * @component App
 * @description
 * - Combines all the main components of the application.
 * - Contains a single hild component eParentLeadListe.
  -->

<template>
  <div class="bg-gray-900 p-8 shadow min-h-screen">
    <!-- Parent component for the entire page component -->
    <ParentLeadList></ParentLeadList>
  </div>
</template>


<script setup>
// Import the parent component
import ParentLeadList from './components/ParentLeadList.vue';
</script>
<style></style>