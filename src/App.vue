<script setup>
// Importando funcion para crear referencias reactivas
import { ref } from 'vue'
//Creando un tipo de referencia reactiva de tipo string
const header = ref('App Lista de Compras');
const shoppingIcon = ref ('material-icons shopping-cart-icon');
// Creando una referencia reactiva para almacenar el valor de la lista
const items = ref ([
  // {id: 0, label:'Leche'}, 
  // {id: 1, label:'Arroz'}, 
  // {id: 2, label:'Carne'}, 
  // {id: 3, label:'Pan'}, 
  // {id: 4, label:'Huevos'}
  ]);
  const newItem = ref('');
  const newItemHightPriority = ref(false);
  const showForm = ref(false);
  // Metodos
  const saveItems = () => {
    // Agrega un nuevo elemento a la lista proveniente de la caja de texto
    items.value.push({id: items.value.length, label: newItem.value})
    // Borramos el contenido de la caja de texto.
    newItem.value=""
    
  };

  const cancelAddItem = () => {
    showForm.value = false;
  };

  const showAddItemForm = () => {
    showForm.value = true;
  };



</script>

<template>
  <!-- Header -->
  <div class="header">
    <h1>
      <i :class="shoppingIcon">local_mall</i>{{ header }}
    </h1>
    <button v-if="showForm" class="btn-cancel" @click="cancelAddItem">Cancelar</button>
    <button v-else class="btn-primary" @click="showAddItemForm">Agregar Articulo</button>
  </div>
  <!-- Formulario -->
  <form
   v-if="showForm" v-on:submit.prevent="saveItems" class="add-item form">
    <input v-model="newItem" type="text" placeholder="Agregar Articulo">
    <!-- Checkbox  -->
    <label><input type="checkbox" v-model="newItemHightPriority" >Alta Prioridad</label>
    <!-- Boton -->
    <button class="btn-primary">Agregar Articulo</button>
  </form>
  <!-- Entrega de Lista -->
  <ul>
   <li v-for="{id, label} in items" v-bind:key="id">⭐ {{ label }}</li>
  </ul>
  <!-- Mensaje Condicional -->
  <p v-if="items.length === 0">🥀No hay elementos en la lista</p>
</template>

<style scoped>
.shopping-cart-icon {
  font-size: 2rem;
}
</style>
