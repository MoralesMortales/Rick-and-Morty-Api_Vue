<template>

  <div v-if="character" class="about">

  <div id="container" class="rounded-2xl w-screen flex justify-center mt-7 p-5">
  
  <div class="w-2/3 bg-gray-500 p-5 rounded-2xl">

  <div class="text-4xl font-serif mb-6 bg" id="title ">
    <h2 class="texto  text-center">{{ character.name }}</h2>
  </div>
  
  <div class="flex justify-around">

  <div class="flex justify-center" id="image">
    <img :src="character.image" alt="" class="rounded-full">
  </div>
  
    <div class="flex flex-col items-center justify-center text-center bg-zinc-600 w-1/2 rounded-lg gap-3">
    <h2 class="texto">El genero es: {{ character.gender }}</h2>
    <h2 class="texto">Su especie es: {{ character.species }}</h2>
    <h2 class="texto">Su estatus es: {{ character.status }}</h2>
    <h2 class="texto">Esta en: {{ character.location.name }}</h2>
    </div>
  
</div>


  </div>
  
</div>

<div class="text-center">
<router-link :to="'/'">
<button class=" w-1/3 bg-black rounded-2xl text-white ">Volver</button>
</router-link>
</div>
  </div>


</template>

<style>
.texto{

color:white;


}

body{

  background-color:rgb(200, 200, 200);

}

</style>

<script setup>
import { useRoute } from 'vue-router';
import { onMounted, ref } from "vue";

const route = useRoute();

const characterId = route.params.id;

const character = ref(null) 

onMounted(async() => {
  try { //cuendo pasa un error intentara esto
    const response = await fetch(`https://rickandmortyapi.com/api/character/${characterId}`);
    const data = await response.json();
    character.value = data; 
    console.log(data)
  }
  catch { //cuando te manda un error
  }
})

</script>