<script setup>
import { onMounted, reactive, watch } from "vue";
import Header from "./components/Header.vue";
import Formulario from "./components/Formulario.vue";
import Paciente from "./components/Paciente.vue";
import { uid } from "uid";

const pacientes = reactive([]);

const paciente = reactive({
    id: null,
    nome: '',
    proprietario: '',
    data: '',
    email: '', 
    sintomas: ''
});
watch(pacientes, () =>{
  salvarLocalStorage()
},{
  deep: true
}
)
const salvarLocalStorage = () =>{
  localStorage.setItem('pacientes', JSON.stringify(pacientes))
}
onMounted(() => {
  const pacientesStorage = localStorage.getItem('pacientes');
  if (pacientesStorage) {
    const pacientesFromStorage = JSON.parse(pacientesStorage);
    pacientes.push(...pacientesFromStorage); // Adiciona os pacientes ao array reativo
  }
});

const salvarPaciente = () => {
    // Reiniciar o formulário
    if (paciente.id) {
        const i = pacientes.findIndex((pacienteState) => pacienteState.id === paciente.id);
        pacientes[i] = { ...paciente };
    } else {
        pacientes.push({ ...paciente, id: uid() });
    }

    // Limpar o formulário
    paciente.id = null; 
    paciente.nome = '';
    paciente.proprietario = '';
    paciente.data = '';
    paciente.email = ''; 
    paciente.sintomas = '';
};

const editarPaciente = (id) => {
    const pacienteEditar = pacientes.find(paciente => paciente.id === id);
    if (pacienteEditar) {
        Object.assign(paciente, pacienteEditar);
    }
};
const eliminarPaciente = (id) => {
  const pacientesFiltrados = pacientes.filter(paciente => paciente.id !== id);
  
  // Modificação do array original
  pacientes.splice(0, pacientes.length, ...pacientesFiltrados);
};


</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />
    <div class="mt-12 md:flex">
      <Formulario 
        v-model:nome="paciente.nome" 
        v-model:proprietario="paciente.proprietario" 
        v-model:email="paciente.email"  
        v-model:data="paciente.data" 
        v-model:sintomas="paciente.sintomas"
        @salvar-paciente="salvarPaciente" 
        @editar-paciente="editarPaciente"
        :id="paciente.id"
      />
      
      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administrar Pacientes</h3>
      
        <div v-if="pacientes.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
            Informação do
            <span class="text-indigo-600 font-bold">Paciente</span>
          </p>
          <Paciente 
            v-for="paciente in pacientes" 
            :key="paciente.id" 
            :paciente="paciente" 
            @editar-paciente="editarPaciente"
            @eliminar-paciente="eliminarPaciente"
          />
        </div>
        <p v-else class="mt-20 text-2xl text-center">Não há pacientes</p>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
