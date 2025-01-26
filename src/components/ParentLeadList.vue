<!--
* Parent component for working with the list of leads.
*
* @component ParentLeadList
* @description
* - Loads a static list of leads.
* - Passes the `leads` array as `props` to the `LeadsList` child component.
*
* @props
* - `leads` (Array): An array of objects with lead data.
-->



<template>
  <div>
    <!-- We pass the list of leads with the binding "contacts" to LeadList -->
    <LeadsList :contacts="leads" />
  </div>
</template>

<script setup>
// Vue's core methods for reactivity and computation
import { ref } from 'vue';
// Import the component displaying the list of leads
import LeadsList from './LeadsList.vue';

// Create a static list of customers that will later be replaced with data from API
const leads = ref([
{
    id: 1,
    sent: "20.01.2025",
    name: "Jan",
    last_name: "Janowski",
    email: "jan.janowski@email.com",
    phone: "+48123456789",
    message: "Dzień dobry, natknąłem się na Państwa produkt i muszę przyznać, że wygląda on bardzo interesująco. W szczególności zwróciłem uwagę na funkcje, które mogą pomóc mi w mojej codziennej pracy. Czy mogliby Państwo przesłać więcej informacji?",
    region: "Zachodniepomorskie",
    website_id: 1,
    score: 0.8,
  },
  {
    id: 2,
    sent: "29.01.2025",
    name: "Katarzyna",
    last_name: "Kowalska",
    email: "katarzyna.kowalska@email.com",
    phone: "+48987654321",
    message: "Proszę o kontakt w sprawie szczegółów produktu. Chciałabym dowiedzieć się więcej o możliwościach integracji oraz o ewentualnych rabatach dla większych zamówień.",
    region: "Mazowieckie",
    website_id: 2,
    score: 0.9,
  },
  {
    id: 3,
    sent: "15.01.2025",
    name: "Adam",
    last_name: "Nowak",
    email: "adam.nowak@email.com",
    phone: "+48111222333",
    message: "Jestem zainteresowany Państwa produktem, jednak chciałbym uzyskać więcej szczegółowych informacji dotyczących funkcjonalności oraz kompatybilności z istniejącymi systemami.",
    region: "Śląskie",
    website_id: 3,
    score: 0.7,
  },
  {
    id: 4,
    sent: "10.01.2025",
    name: "Ewa",
    last_name: "Kaczmarek",
    email: "ewa.kaczmarek@email.com",
    phone: "+48555666777",
    message: "Potrzebuję więcej informacji o Państwa produkcie, szczególnie w kontekście jego zastosowania w mojej branży. Proszę o kontakt w najbliższym możliwym terminie.",
    region: "Wielkopolskie",
    website_id: 1,
    score: 0.85,
  },
  {
    id: 5,
    sent: "25.01.2025",
    name: "Piotr",
    last_name: "Lewandowski",
    email: "piotr.lewandowski@email.com",
    phone: "+48222333444",
    message: "Interesuję się produktem 3. Czy mogliby Państwo przesłać mi szczegółowy katalog wraz z cenami? Jestem zainteresowany współpracą długoterminową.",
    region: "Małopolskie",
    website_id: 2,
    score: 0.95,
  },
  {
    id: 6,
    sent: "22.01.2025",
    name: "Anna",
    last_name: "Zielińska",
    email: "anna.zielinska@email.com",
    phone: "+48999888777",
    message: "Proszę o przesłanie oferty wraz z dodatkowymi materiałami na temat funkcji produktu. Szczególnie interesują mnie możliwości integracji z innymi systemami.",
    region: "Pomorskie",
    website_id: 3,
    score: 0.75,
  },
  {
    id: 7,
    sent: "12.01.2025",
    name: "Tomasz",
    last_name: "Wiśniewski",
    email: "tomasz.wisniewski@email.com",
    phone: "+48777888999",
    message: "Chciałbym uzyskać więcej informacji na temat Państwa produktu. Interesuje mnie, jakie są dostępne opcje personalizacji i jakie są koszty wdrożenia.",
    region: "Łódzkie",
    website_id: 1,
    score: 0.65,
  },
  {
    id: 8,
    sent: "05.01.2025",
    name: "Zofia",
    last_name: "Dąbrowska",
    email: "zofia.dabrowska@email.com",
    phone: "+48666555444",
    message: "Chcę umówić spotkanie w sprawie produktu. Proszę o kontakt w celu ustalenia dogodnego terminu. Jestem szczególnie zainteresowana szczegółami dotyczącymi Państwa oferty.",
    region: "Lubelskie",
    website_id: 2,
    score: 0.9,
  },
  {
    id: 9,
    sent: "18.01.2025",
    name: "Michał",
    last_name: "Kwiatkowski",
    email: "michal.kwiatkowski@email.com",
    phone: "+48567890123",
    message: "Jestem zainteresowany możliwością długoterminowej współpracy. Proszę o przesłanie oferty oraz przykładów realizacji.",
    region: "Podkarpackie",
    website_id: 3,
    score: 0.85,
  },
  {
    id: 10,
    sent: "19.01.2025",
    name: "Joanna",
    last_name: "Baran",
    email: "joanna.baran@email.com",
    phone: "+48765432109",
    message: "Czy mogę prosić o katalog produktów? Chciałabym zobaczyć pełną ofertę i porównać dostępne opcje.",
    region: "Świętokrzyskie",
    website_id: 1,
    score: 0.8,
  },
  {
    id: 11,
    sent: "16.01.2025",
    name: "Rafał",
    last_name: "Wojciechowski",
    email: "rafal.wojciechowski@email.com",
    phone: "+48901234567",
    message: "Proszę o informacje dotyczące wdrożenia Państwa produktu w naszej firmie. Interesuje mnie również, jakie są warunki gwarancji.",
    region: "Podlaskie",
    website_id: 2,
    score: 0.78,
  },
  {
    id: 12,
    sent: "17.01.2025",
    name: "Agnieszka",
    last_name: "Szymańska",
    email: "agnieszka.szymanska@email.com",
    phone: "+48654321098",
    message: "Chcę porozmawiać o możliwościach dostosowania Państwa produktu do naszych potrzeb. Proszę o kontakt telefoniczny.",
    region: "Lubuskie",
    website_id: 3,
    score: 0.82,
  },
  {
    id: 13,
    sent: "21.01.2025",
    name: "Paweł",
    last_name: "Nowicki",
    email: "pawel.nowicki@email.com",
    phone: "+48876543210",
    message: "Czy mogę liczyć na zniżki przy większym zamówieniu? Proszę o kontakt w tej sprawie.",
    region: "Opolskie",
    website_id: 1,
    score: 0.9,
  },
  {
    id: 14,
    sent: "14.01.2025",
    name: "Sylwia",
    last_name: "Kamińska",
    email: "sylwia.kaminska@email.com",
    phone: "+48712345678",
    message: "Mam kilka pytań dotyczących specyfikacji technicznej produktu. Proszę o kontakt mailowy.",
    region: "Dolnośląskie",
    website_id: 2,
    score: 0.8,
  },
  {
    id: 15,
    sent: "13.01.2025",
    name: "Krzysztof",
    last_name: "Kozłowski",
    email: "krzysztof.kozlowski@email.com",
    phone: "+48987654321",
    message: "Interesuje mnie Państwa produkt w kontekście zastosowania w branży budowlanej. Czy mogę prosić o przykłady wdrożeń?",
    region: "Kujawsko-Pomorskie",
    website_id: 3,
    score: 0.87,
  },
  {
    id: 16,
    sent: "23.01.2025",
    name: "Monika",
    last_name: "Pawlak",
    email: "monika.pawlak@email.com",
    phone: "+48123409876",
    message: "Czy mogę prosić o pełny opis funkcji produktu? Chciałabym lepiej zrozumieć możliwości, jakie oferuje.",
    region: "Warmińsko-Mazurskie",
    website_id: 2,
    score: 0.88,
  },
]);
</script>
