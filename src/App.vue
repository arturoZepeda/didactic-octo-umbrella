
<script setup>
import { ref,reactive} from 'vue';
import Cabecera from './component/Cabecera.vue';
import Formulario from './components/Formulario.vue';

const pacientes = ref([]);

const paciente = reactive({
    nombre: '',
    propietario: '',
    telefono: '',
    email: '',
    fecha: '',
    sintomas: ''
});

const guardarPaciente = () => {
    pacientes.value.push({...paciente});
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
        
        </div>
        <div v-else class="text-center text-gray-500">No hay pacientes agregados</div>
      </div>
    </div>
  </div>
</template>

