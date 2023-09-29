<template>
  <div class="container">
    <button 
    @click="goToFormulario"
    class="btn btn-success my-2">AGREGAR</button>
    <Tabla />
  </div>
</template>

<script setup lang="ts">
import Tabla from '@/components/Tabla.vue';
import { useRouter } from 'vue-router';

const router = useRouter();
const goToFormulario = ()=>{
  router.push('/crud-formulario')
}
</script>

<style scoped></style>
