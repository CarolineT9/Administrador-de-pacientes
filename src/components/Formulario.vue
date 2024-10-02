<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Consultas Pacientes</h2>
        <p class="text-lg mt-5 text-center mb-10">
            Adicionar pacientes e 
            <span class="text-indigo-600 font-bold">Administrá-los</span>
        </p>

        <Alerta v-if="alerta.mensagem" :alerta="alerta"/>
       
        <form class="bg-white shadow-md rounded-lg py-10 px-5 mb-10" @submit.prevent="validar">
            <div class="mb-5">
                <label class="block text-gray-700 uppercase font-bold" for="pet">Nome do Pet</label>
                <input 
                    :value="nome" 
                    @input="$emit('update:nome', $event.target.value)" 
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" 
                    id="pet" 
                    type="text" 
                    placeholder="Nome do pet"
                />
            </div>
            <div class="mb-5">
                <label class="block text-gray-700 uppercase font-bold" for="proprietario">Nome do Proprietário</label>
                <input 
                    :value="proprietario" 
                    @input="$emit('update:proprietario', $event.target.value)"  
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" 
                    id="proprietario" 
                    type="text" 
                    placeholder="Nome do proprietário"
                />
            </div>
            <div class="mb-5">
                <label class="block text-gray-700 uppercase font-bold" for="email">Email</label>
                <input 
                    :value="email" 
                    @input="$emit('update:email', $event.target.value)"  
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" 
                    id="email" 
                    type="email" 
                    placeholder="Email"
                />
            </div>
            <div class="mb-5">
                <label class="block text-gray-700 uppercase font-bold" for="data">Data de Entrada</label>
                <input 
                    :value="data" 
                    @input="$emit('update:data', $event.target.value)"  
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md" 
                    id="data" 
                    type="date" 
                />
            </div>
            <div class="mb-5">
                <label class="block text-gray-700 uppercase font-bold" for="sintomas">Sintomas</label>
                <textarea 
                    :value="sintomas" 
                    @input="$emit('update:sintomas', $event.target.value)" 
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md h-40" 
                    id="sintomas" 
                    placeholder="Descreva os sintomas do paciente"
                />
            </div>
            <input 
                type="submit" 
                class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors" 
                :value="[editando ? 'Salvar mudanças' : 'Registrar paciente']" 
            />
        </form>
    </div>
</template>


<script setup>
import { reactive, defineEmits, defineProps, computed } from 'vue';
import Alerta from './Alerta.vue';

const alerta = reactive({
    tipo: '',
    mensagem: ''
});

const props = defineProps({
    nome: {
        type: String,
        required: true
    },
    proprietario: {
        type: String,
        required: true
    },
    email: {
        type: String,
        required: true
    },
    data: {
        type: String,
        required: true
    },
    sintomas: {
        type: String,
        required: true
    },
    id:{
        type: [String,null],
        required: true
    }
});

const emit = defineEmits(['update:nome', 'update:proprietario', 'update:email', 'update:data', 'update:sintomas', 'salvar-paciente']);

const validar = () => {
    if (Object.values(props).includes('')) {
        alerta.mensagem = 'Todos os campos são obrigatórios';
        alerta.tipo = 'error';
        return;
    }
    emit('salvar-paciente')
    alerta.mensagem = 'Paciente cadastrado!';
    alerta.tipo === 'exito'

    setTimeout(() =>{
        Object.assign(alerta,{
            tipo: '',
            mensagem: ''
        })
    },3000)

}

const editando = computed(() => {
    return props.id
})

</script>


<style>

</style>