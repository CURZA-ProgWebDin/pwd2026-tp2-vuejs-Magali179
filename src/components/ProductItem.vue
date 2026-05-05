<template>
    <li class="item">
      <span class="texto">
      id: {{ producto.id }} - {{ producto.name }} - Precio: ${{ producto.price }} - Stock: {{ producto.stock }} - Categoria: {{ producto.categoria }}
      </span>
      <button @click="eliminar" class="eliminar">Eliminar</button>
    </li>

</template>



<script setup>
const props = defineProps({
    producto: Object,
   
})
const emit = defineEmits(['eliminar'])
function eliminar() {
    emit('eliminar', props.producto.id)
}

</script>

<style scope> 

.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}

.texto {
  flex: 1;
}

.eliminar {
  margin-left: 20px; 
  background-color: red;
  color: white;
  border: none;
  padding: 5px 12px;
  font-size: 12px;
  border-radius: 4px;
  cursor: pointer;
  width: auto;
}
.eliminar:hover {
  background-color: darkred;
}
li {
  display: flex;
  justify-content: space-between; /* 🔥 separa texto y botón */
  align-items: center;
}

 </style>