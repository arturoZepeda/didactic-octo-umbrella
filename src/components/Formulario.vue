<script setup>  
import { reactive } from 'vue';
import Alerta from './Alerta.vue';

const alerta = reactive({
    tipo: '',
    mensaje: ''
});

const paciente = reactive({
    nombre: '',
    propietario: '',
    telefono: '',
    email: '',
    fecha: '',
    sintomas: ''
});

const validar = () => {
    if(Object.values(paciente).includes('')){
        alerta.mensaje = 'Todos los campos son obligatorios';
        alerta.tipo = 'error';
        return;
    }
    console.log('Todo bien');
}    

</script>
<template>
<div class="md:w-1/2">
    <h2 class="font-black text-3xl text-center"> Seguimiento Pacientes</h2>
    <p class="text-lg mt-5 text-center mb-10">
        Añade pacientes y
        <span class="text-indigo-600 font-bold" >
            Administralos
        </span>
    </p>
    <Alerta
    v-if="alerta.mensaje"
    :alerta="alerta"
    />
    <form
        class="bg-white rounded-lg shadow-md py-10 px-5 mb-10"
        @submit.prevent="validar">
        <div class="mb-5">
            <label
                for="mascota"
                class="block text-gray-700 uppercase font-bold">
                Nombre Mascota
            </label>
            <input id="mascota"
                type="text"
                placeholder="Nombre Mascota"
                class="border-2 w-full p-2 pt-2 placeholder-gray-400 rounded-md"
                v-model="paciente.nombre">
        </div>
        <div>
            <label
                for="propietario"
                class="block text-gray-700 uppercase font-bold">
                Nombre Propietario
            </label>
            <input id="propietario"
                type="text"
                placeholder="Nombre del Propietario"
                class="border-2 w-full p-2 pt-2 placeholder-gray-400 rounded-md"
                v-model="paciente.propietario">
        </div>
        <div>
            <label
                for="telefono"
                class="block text-gray-700 uppercase font-bold">
                Teléfono
            </label>
            <input id="telefono"
                type="tel"
                placeholder="Teléfono"
                class="border-2 w-full p-2 pt-2 placeholder-gray-400 rounded-md"
                v-model="paciente.telefono">
        </div>
        <div>
            <label
                for="email"
                class="block text-gray-700 uppercase font-bold">
                Email
            </label>
            <input id="email"
                type="email"
                placeholder="Email"
                class="border-2 w-full p-2 pt-2 placeholder-gray-400 rounded-md"
                v-model="paciente.email">
        </div>
        <div>
            <label
                for="alta"
                class="block text-gray-700 uppercase font-bold">
                Alta
            </label>
            <input id="alta"
                type="date"
                class="border-2 w-full p-2 pt-2 placeholder-gray-400 rounded-md"
                v-model="paciente.fecha">
        </div>
        <div>
            <label
                for="sintomas"
                class="block text-gray-700 uppercase font-bold">
                Síntomas
            </label>
            <textarea id="sintomas"
                class="border-2 w-full p-2 pt-2 placeholder-gray-400 rounded-md"
                v-model="paciente.sintomas"></textarea>
        </div>
        <input type="submit"
            value="Agregar Paciente"
            class="bg-indigo-500 w-full mt-5 p-2 text-white uppercase font-bold hover:bg-indigo-600 transition-colors">
    </form>
</div>
</template>
