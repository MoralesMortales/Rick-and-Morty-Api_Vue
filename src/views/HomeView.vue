<script setup>

import { ref } from 'vue';
import card from "../components/card.vue";

/* cammelcase, snakecase */

let character = ref([]);
let page = ref(1)

function nextpage() {
  page.value++;
  loadCharacters()
}

function backpage() {
  page.value--;
  loadCharacters()
}

async function loadCharacters() {
  const response = await fetch(`https://rickandmortyapi.com/api/character?page=${page.value}`);
  const data = await response.json();
  character.value = data.results;
  console.log(data);
}

loadCharacters();

</script>

<template>

  <div class="m-8 flex justify-center flex-col" id="container">

    <div class="flex justify-center mb-10 py-7 text-nowrap">
      <h1 class="lg:text-5xl text-2xl md:text-5xl text-rose-950">Rick and Morty API</h1>
    </div>

    <div class="mb-8 grid sm:grid-cols-1 sm:items-center sm:justify-items-center md:grid-cols-3 lg:grid-cols-4 gap-12 mx-auto">
    

      <router-link v-for="personaje in character" :key="character.id" class="bg-red-700 flex hover:scale-105 max-w-80 h-full justify-center text-center rounded-lg shadow-black shadow-md" :to="`/${personaje.id}`">
        <card :character="personaje"/>
      </router-link>
    </div>

    <div class="flex flex-row justify-around items-center">
      <div class="w-1/3 flex justify-center">
        <button @click="backpage" :disabled="page === 1" class="p-5 rounded-lg bg-black text-white hover:transition hover:bg-slate-800 transition-all">Go to previous page</button>      
      </div>
      <div class="w-1/3 flex justify-center">
        <span class="bg-white rounded-full px-5 py-3"> {{ page }} </span>
      </div>
      <div class="w-1/3 flex justify-center ">
        <button @click="nextpage" class="p-5 rounded-lg bg-black text-white hover:transition hover:bg-slate-800 transition-all">Go to next page</button>
      </div>
        
    </div>
<!-- : para condiciones especiales z para clases de css -->
  </div>


  </template>
