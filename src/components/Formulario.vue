<template>
  <div class="card mx-auto mt-5" style="width: 350px">
    <form @submit.prevent="procesarFormulario" class="card-body">
      <h1>{{ crud  ? 'Editar':'Agregar' }} Crud</h1>
      <input
        class="form-control mb-2"
        type="text"
        v-model="formData.nombre"
        placeholder="Nombre"
        required
      >
      <input
        type="text"
        placeholder="Descripcion"
        v-model="formData.descripcion"
        class="form-control mb-3"
        required
      >
      <button :disabled="cargando" class="btn btn-primary w-100">Guardar</button>
    </form>
    {{ crud }}
  </div>
</template>

<script setup lang="ts">
import { computed, onMounted, reactive, ref, watch} from 'vue';
import { API, ICrud } from "@/contantes";
import { useRouter } from 'vue-router';

const props = defineProps({
  crud:{
    type: Object as ()=> ICrud | null,
    default: null
  }
})
const formData = reactive({
  nombre:'',
  descripcion:''
})
const cargando = ref(false)
const router = useRouter()
const crud = computed(()=> props.crud)

watch(crud, ()=> {
  formData.nombre = crud.value.name
  formData.descripcion = crud.value.description
})

const procesarFormulario = async()=>{
  cargando.value = true;
  if(crud.value){
    await fetch(`${API}/api/crud/${crud.value._id}`, {
    method: 'PATCH',
    body: JSON.stringify({name:formData.nombre, description: formData.descripcion }),
    headers: {
      'Content-Type': 'application/json'
    }
  })
  }else{
    await fetch(`${API}/api/crud`,{
    method: 'POST',
    body: JSON.stringify({name:formData.nombre, description: formData.descripcion }),
    headers: {
      'Content-Type': 'application/json'
  }
})
}
  // console.log('Respuesta de API', response)
  cargando.value = false;
  router.back()
}
</script>

<style scoped></style>
