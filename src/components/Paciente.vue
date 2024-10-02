<template>
    <div class="mx-5 my-10 bg-white shadow-md px-5 py-10 rounded-xl">
        <p class="font-bold mb-3 text-gray-700 uppercase">ID:
            <span class="font-normal normal-case">
                {{ paciente.id }}
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Nome:
            <span class="font-normal normal-case">
                {{ paciente.nome }}
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Proprietário: 
            <span class="font-normal normal-case">
                {{ paciente.proprientario }}
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Email: 
            <span class="font-normal normal-case">
                {{ paciente.email }}
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Data entrada:
            <span class="font-normal normal-case">
                {{ paciente.data }}
            </span>
        </p>

        <p class="font-bold mb-3 text-gray-700 uppercase">Sintomas:
            <span class="font-normal normal-case">
                {{ paciente.sintomas }}
            </span>
        </p>

        <div class="grid md:grid-cols-2  gap-5 mt-10 ">
            <button @click="emit('editar-paciente', paciente.id)"
                type="button"
                class="block w-full py-2 px-10 bg-indigo-600 hover:bg-indigo-700 text-white font-bold uppercase rounded-lg"
            >Editar</button>

            <button 
                type="button"
                class="block w-full py-2 px-10 bg-red-600 hover:bg-red-700 text-white font-bold uppercase rounded-lg" @click="$emit('eliminar-paciente', paciente.id)"
            >Excluir</button>
        </div>
    </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
    paciente:{
        type: Object,
        required: true
    }
})
const emit = defineEmits (['editar-paciente', 'eliminar-paciente'])
</script>