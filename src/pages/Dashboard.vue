<template>
  <div class="flex h-screen bg-black text-white">
    <Loader :isLoading="loading" />
    <Sidebar @section-change="handleSectionChange" />    
    <!-- Main Content -->
    <main class="flex-grow p-8 overflow-auto">
      <header class="mb-8">
        <h2 class="text-2xl font-bold">{{$t("hello")}}, {{ username }}</h2>
        <p class="text-lg">{{ $t('welcomeback') }} 🎉</p>
      </header>
      <router-view />
    </main>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import Sidebar from '../components/Sidebar.vue';
import { useRouter } from 'vue-router';
import AuthService from '../services/AuthService';
import Loader from '../components/Loader.vue';
import loading from '../store/loadingState'; // Importar el estado global de loading

const username = (new AuthService()).userLogged().username; // Replace with actual username logic
const currentSection = ref('Crypto');
const selectedSymbol = ref('');

const handleSectionChange = (section) => {
  currentSection.value = section;
  selectedSymbol.value = ''; // Reset symbol filter when changing sections
};
</script>

<style>
@import 'tailwindcss/base';
@import 'tailwindcss/components';
@import 'tailwindcss/utilities';
</style>
