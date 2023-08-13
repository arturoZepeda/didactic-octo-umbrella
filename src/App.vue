
<script setup>
import { ref,reactive, watch, onMounted} from 'vue';
import { uid } from 'uid';

import Cabecera from './components/Cabecera.vue';
import Formulario from './components/Formulario.vue';
import Paciente from './components/Paciente.vue';

const pacientes = ref([]);

onMounted(() => {
  const pacientesLS = JSON.parse(localStorage.getItem('pacientes'));
  if (pacientesLS) {
    pacientes.value = pacientesLS;
  }
});

const paciente = reactive({
    id: null,
    nombre: '',
    propietario: '',
    telefono: '',
    email: '',
    fecha: '',
    sintomas: ''
});

watch(pacientes, () => {
  guardarLocalStorage();
}, { deep: true });

const eliminarPaciente =( id ) => {
  const index = pacientes.value.findIndex(paciente => paciente.id === id);
  pacientes.value.splice(index, 1);
}

const guardarPaciente = () => {
    if  (paciente.id) {
      const { id } = paciente;
      const index = pacientes.value.findIndex(paciente => paciente.id === id);
      pacientes.value.splice(index, 1, paciente);
      return;
    }else{
    pacientes.value.push({
      ...paciente, id: uid()
    });
    }
    paciente.nombre = '';
    paciente.propietario = '';
    paciente.telefono = '';
    paciente.email = '';
    paciente.fecha = '';
    paciente.sintomas = '';
}

const actualizarPaciente = (id) => {
  const pacienteEditar = pacientes.value.filter(paciente => paciente.id === id)[0];
  console.log(pacienteEditar);
  Object.assign(paciente, pacienteEditar);
}

const guardarLocalStorage = () => {
  localStorage.setItem('pacientes', JSON.stringify(pacientes.value));
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
        :id="paciente.id"
      />
      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-2xl text-center mb-5">Administra tus pacientes</h3>
        <div v-if="pacientes.length>0">
          <p class="text-center text-gray-500 mb-5">Información de <span class="text-indigo-600 font-bold" >Pacientes</span></p> 
          <paciente 
          v-for="paciente in pacientes"
          :paciente="paciente"
          @actualizar-paciente="actualizarPaciente"
          @eliminar-paciente="eliminarPaciente"
          >

          </paciente>
        </div>
        <div v-else class="text-center text-gray-500">No hay pacientes agregados</div>
      </div>
    </div>
  </div>
</template>

