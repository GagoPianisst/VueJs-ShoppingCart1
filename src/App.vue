<script setup>
// Importando funcion para crear referencias reactivas
import { ref, computed } from 'vue'
//Creando un tipo de referencia reactiva de tipo string
const header = ref('App Lista de Compras');
const shoppingIcon = ref ('material-icons shopping-cart-icon');
// Creando una referencia reactiva para almacenar el valor de la lista
const items = ref ([
  // {id: 0, label:'Leche', purchased: false, highPriority: true}, 
  // {id: 1, label:'Arroz', purchased: false, highPriority: false }, 
  // {id: 2, label:'Carne', purchased: true, highPriority: false}, 
  // {id: 3, label:'Pan', purchased: false, highPriority: true}, 
  // {id: 4, label:'Huevos', purchased: true, highPriority: true}
  ]);
  const reverseItems = computed(()=> {
    //Regresar una version invertida del arreglo items
    return [...items.value]. reverse()
  })
  const togglePurchased = (item) => {
    item.purchased = !item.purchased
  };
  const newItem = ref('');
  //Creamdp propiedad computada
  const characterCount = computed(()=>{
    return newItem.value.length;
  });
  const newItemHightPriority = ref(false);
  const showForm = ref(false);
  // Metodos
  const saveItems = () => {
    // Agrega un nuevo elemento a la lista proveniente de la caja de texto
    items.value.push({id: items.value.length, label: newItem.value, highPriority: newItemHightPriority.value})
    // Borramos el contenido de la caja de texto.
    newItem.value=""
    newItemHightPriority.value="false";
    
  };

  const cancelAddItem = () => {
    showForm.value = false;
    newItemHightPriority.value="false";
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
    <p class="counter">
      {{ characterCount }} / 200
    </p>
  </form>
  <!-- Entrega de Lista -->
  <ul>
   <li 
   v-for="({id, label, purchased, highPriority}, index) in reverseItems" 
   @click="togglePurchased(reverseItems[index])"
   :class="{priority: highPriority,strikeout: purchased}"
   v-bind:key="id">
   ⭐ {{ label }}
   </li>
  </ul>
  <!-- <ul>
   <li 
   v-for="{id, label, purchased, highPriority} in items" 
   :class="[purchased ? 'strikeout' : '', highPriority ? 'priority' : '']"
   v-bind:key="id">
   ⭐ {{ label }}
   </li>
  </ul> -->
  <!-- Mensaje Condicional -->
  <p v-if="items.length === 0">🥀No hay elementos en la lista</p>
</template>

<style scoped>
.shopping-cart-icon {
  font-size: 2rem;
}
</style>
