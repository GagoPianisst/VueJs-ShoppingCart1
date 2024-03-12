<script setup>
// Importando funcion para crear referencias reactivas
import { ref } from 'vue'
//Creando un tipo de referencia reactiva de tipo string
const header = ref('App Lista de Compras');
const shoppingIcon = ref ('material-icons shopping-cart-icon');
// Creando una referencia reactiva para almacenar el valor de la lista
const items = ref ([
  {id: 0, label:'Leche'}, 
  {id: 1, label:'Arroz'}, 
  {id: 2, label:'Carne'}, 
  {id: 3, label:'Pan'}, 
  {id: 4, label:'Huevos'}
  ]);
  const newItem = ref('');
  const newItemHightPriority = ref(false);
  // Metodos
  const saveItems = () => {
    // Agrega un nuevo elemento a la lista proveniente de la caja de texto
    items.value.push({id: items.value.length, label: newItem.value})
    // Borramos el contenido de la caja de texto.
    newItem.value=""
  };
</script>

<template>
  <h1><i :class="shoppingIcon">local_mall</i>{{ header }}</h1>
  <form v-on:submit.prevent="saveItems" class="add-item form">
    <input v-model="newItem" type="text" placeholder="Agregar Articulo">
    <!-- Checkbox  -->
    <label><input type="checkbox" v-model="newItemHightPriority" >Alta Prioridad</label>
    <!-- Boton -->
    <button class="btn-primary">Agregar Articulo</button>
  </form>
  <ul>
   <li v-for="{id, label} in items" v-bind:key="id">⭐ {{ label }}</li>
  </ul>
</template>

<style scoped>
.shopping-cart-icon {
  font-size: 2rem;
}
</style>
