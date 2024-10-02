<template>
    <div :class="[isError ? 'bg-red-500' : 'bg-green-500' ] " class="text-white text-center p-3 uppercase font-bold mb-3 rounded-md">
        {{alerta.mensagem}}
    </div>
  
</template>

<script setup>
import { defineProps, computed } from 'vue';
const props = defineProps({
    alerta: {
        type:Object,
        required: true
    }
})
const isError = computed(() =>{
   return props.alerta.tipo === 'error'
})
</script>

<style>

</style>