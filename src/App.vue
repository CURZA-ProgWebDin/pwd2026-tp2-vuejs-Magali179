<template>

<ProductForm @crear-producto="agregarProducto"/>
<h3>Mostrar productos</h3>
<select v-model="Filtro" >
    <option value="todos">Todos</option>
    <option value="Elect">Electronica</option>
    <option value="Lib">Libreria</option>
    <option value="Limp">Limpieza</option>

</select>
    <h3>Total productos: {{ totalProductos }}</h3>
    <p>Total de productos en stock: {{ totalStock }} </p>
    <p>Total del valor de inventario: ${{ totalValorInventario }}</p>
<ProductList :lista="productosFiltrados" @eliminar="eliminarProducto"/>



</template>



<script setup>
import {ref,computed} from 'vue'
import ProductForm from './components/ProductForm.vue'
import ProductList from './components/ProductList.vue'

const productos = ref([])
const Filtro = ref('todos')
let idCounter = 1

const productosFiltrados = computed(() => {
    if (Filtro.value === 'todos') {
        return productos.value
    }
    return productos.value.filter(producto => producto.categoria === Filtro.value)
})

function agregarProducto(nuevoProducto) {
nuevoProducto.id = idCounter++
productos.value.push(nuevoProducto)
}
function eliminarProducto(id) {
    productos.value = productos.value.filter(producto => producto.id !== id)
}
const totalProductos = computed(() => productos.value.length)
const totalStock = computed(() => productos.value.reduce((total, producto) => total + producto.stock, 0))
const totalValorInventario = computed(() => productos.value.reduce((total, producto) => total + (producto.price * producto.stock), 0))

</script>



<style scope></style>