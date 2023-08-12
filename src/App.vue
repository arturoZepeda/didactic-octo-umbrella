
<script setup>
import { ref,reactive} from 'vue';
import { uid } from 'uid';

import Cabecera from './components/cabecera.vue';
import Formulario from './components/Formulario.vue';
import Paciente from './components/Paciente.vue';

const pacientes = ref([]);

const paciente = reactive({
    id: null,
    nombre: '',
    propietario: '',
    telefono: '',
    email: '',
    fecha: '',
    sintomas: ''
});

const guardarPaciente = () => {
    pacientes.value.push({
      ...paciente, id: uid()
    });
    paciente.nombre = '';
    paciente.propietario = '';
    paciente.telefono = '';
    paciente.email = '';
    paciente.fecha = '';
    paciente.sintomas = '';
}

</script>

<template>
  <div class="container mx-auto mt-20">
    <Cabecera />
    <div class="mt-12 md:flex">
      <Formulario 
        v-model:nombre="paciente.nombre"
        v-model:propietario="paciente.propietario"
        v-model:telefono="paciente.telefono"
        v-model:email="paciente.email"
        v-model:fecha="paciente.fecha"
        v-model:sintomas="paciente.sintomas"
        @guardar-paciente="guardarPaciente"
      />
      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-2xl text-center mb-5">Administra tus pacientes</h3>
        <div v-if="pacientes.length>0">
          <p class="text-center text-gray-500 mb-5">Información de <span class="text-indigo-600 font-bold" >Pacientes</span></p> 
          <paciente 
          v-for="paciente in pacientes"
          :paciente="paciente"
          >

          </paciente>
        </div>
        <div v-else class="text-center text-gray-500">No hay pacientes agregados</div>
      </div>
    </div>
  </div>
</template>

