<template>
  <div class="container">
    <Formulario
      :crud="crud"
    />
  </div>
</template>

<script setup lang="ts">
import Formulario from '@/components/Formulario.vue';
import{ API, type ICrud } from '@/contantes';
import { onBeforeMount, ref } from 'vue';
import {useRoute} from "vue-router";

const {params} = useRoute()
const crud = ref<null | ICrud>(null)

onBeforeMount(async()=>{
  if(params.id){
    const data = await fetch(`${API}/api/crud/${params.id}`)
    crud.value = await data.json()
  }
})
console.log(params)
</script>

<style scoped>

</style>