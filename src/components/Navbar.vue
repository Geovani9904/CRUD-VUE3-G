<template>
  <nav class="navbar bg-body-tertiary">
    <div class="container-fluid">
      <h3 class="navbar-brand">CRUD</h3>
      <div>
        <RouterLink exact-active-class="activo" class="me-2" to="/">Home</RouterLink>
        <RouterLink exact-active-class="activo" to="/crud">CRUD</RouterLink>
      </div>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { RouterLink } from 'vue-router'
</script>

<style scoped>
.activo{
    color: blueviolet;
}
</style>
