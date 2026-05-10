<template>
    <h3>Lista de Productos</h3>

    <div v-if="props.productos.length === 0">
        <p>No hay productos disponibles.</p>
    </div>
    <ul>
        <ProductItem 
            v-for="producto in props.productos" 
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
    productos: Array,
})
const emit = defineEmits(['eliminar'])


function eliminarProducto(id) {
    emit('eliminar', id)
}


</script>

<style scope>   </style>