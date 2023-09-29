<template>
  <div class="card">
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Nombre</th>
          <th scope="col">Descripcion</th>
          <th scope="col">Estado</th>
          <th scope="col">Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="crud in cruds" :key="crud._id">
          <!-- <th scope="row">1</th> -->
          <td>{{ crud.name }}</td>
          <td>{{ crud.description }}</td>
          <td>
            {{ crud.status ? 'pendiente':'realizada' }}
          </td>
          <td>
            <span @click="editar(crud._id)" class="icono"> 
              ✏️ 
            </span>
            <span @click="eliminar(crud)" class="icono"> ❎ </span>
          </td>
        </tr>
      </tbody>
    </table>
    {{ cruds }}
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { API,ICrud } from '@/contantes'
import { useRouter } from 'vue-router'

const cruds = ref<ICrud[]>([])
const router = useRouter();


const   editar = (id:string)=>{
  router.push(`/crud-formulario/${id}`)
}

const eliminar = async ({name, _id}:ICrud)=>{
  const respuesta = confirm(`¿Estas seguro de eliminar este usuario a ${name}?`)
  if(respuesta){
    const data = await fetch(`${API}/api/crud/${_id}`,{
      method:'DELETE'
    })
    const crud = await data.json()
    if(crud){
      cruds.value = cruds.value.filter(x => x._id !== _id)
    }
  }
}

onMounted(async()=>{
  const data = await fetch(`${API}/api/crud`)
  cruds.value = await data.json()
})
</script>

<style scoped>
.icono {
  cursor: pointer;
}
</style>
