<script setup>


import { defineProps } from 'vue'; 
    const props = defineProps({
        character: {
            require: true,
            type: Object
     } 
    })

</script>

<template>
    
    <div class="flex flex-col justify-between">
        <div>
            <img :src="character.image" alt="Image" class="p-4">
        </div>
        
        <div class="p-5 text-3xl items-center h-full flex justify-center">
            <h3>{{character.name}}</h3>
        </div>

    </div>
</template>
