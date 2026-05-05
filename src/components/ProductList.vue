<template>
    <h3>Lista de Productos</h3>

    <div v-if="state.lista.length === 0">
        <p>No hay productos disponibles.</p>
    </div>
    <ul>
        <ProductItem 
            v-for="producto in state.lista" 
            :key="producto.id" 
            :producto="producto" 
           
            @eliminar="eliminarProducto"
        />
    </ul>
</template>

<script setup>
import {reactive, watch} from 'vue'
import ProductItem from './ProductItem.vue'

const props = defineProps({
    lista: Array,
})
const emit = defineEmits(['eliminar'])
const state = reactive({
    lista: props.lista
})
watch(() => props.lista, (newLista) => {
    state.lista = newLista
})
function eliminarProducto(id) {
    emit('eliminar', id)
}


</script>

<style scope>   </style>