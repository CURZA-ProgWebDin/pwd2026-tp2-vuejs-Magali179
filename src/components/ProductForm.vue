<template>
    <h1>Formulario de Productos</h1>
<form @submit.prevent="submitForm">
    <div>
        <label for="name">Nombre producto:</label>
        <input type="text"  id="name" v-model="name" required>
    </div>
    <div>
        <label for="price">Precio producto:</label>
        <input type="number" id="price" v-model="price" required>
    </div>
    <div>
        <label for="stock">Stock:</label>
        <input type="number" id="stock" v-model="stock" required>
    </div>
    <label for="categorias">Categoria:</label>
    <select id="categorias" v-model="categoria" required>
        <option value="Elect">Electronica</option>
        <option value="Lib">Libreria</option>
        <option value="Limp">Limpieza</option>

    </select>
    <div>
    <button type="submit">Agregar Producto</button>
    </div>
</form>

</template>



<script setup>
import {reactive, ref} from 'vue'
const emit = defineEmits(['crear-producto'])

const name = ref('')
const price = ref('')
const stock = ref('')
const categoria = ref('')


const categorias = ref(['Electronica', 'Libreria', 'Limpieza'])

function limpiarFormulario(){
    name.value = ''
    price.value = ''    
    stock.value = ''
    categoria.value = ''
}

function submitForm(){
    if(!name.value || !price.value || !stock.value || !categoria.value){
        alert('Por favor, complete todos los campos')
        return  
    }
    if(isNaN(price.value) || isNaN(stock.value) || (price.value <= 0) || (stock.value < 0)){
        alert('Por favor, ingrese valores válidos para precio y stock')
        return
    }
    const nuevoProducto = {
        name: name.value,
        price: Number(price.value),
        stock: Number(stock.value),
        categoria: categoria.value
    }
    emit('crear-producto', nuevoProducto)
    limpiarFormulario()
  }



 
 
</script>

<style scope>  
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

/* Fondo general */
body {
  background: linear-gradient(135deg, #667eea, #764ba2);
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Contenedor principal */
.container {
  background: white;
  padding: 30px;
  border-radius: 12px;
  width: 350px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
}

/* Título */
h1 {
  text-align: center;
  margin-bottom: 20px;
  color: #333;
}

/* Labels */
label {
  display: block;
  margin-bottom: 5px;
  font-weight: 600;
  color: #555;
}

/* Inputs y select */
input,
select {
  width: 100%;
  padding: 10px;
  margin-bottom: 15px;
  border-radius: 8px;
  border: 1px solid #ccc;
  transition: 0.3s;
}

/* Focus */
input:focus,
select:focus {
  border-color: #667eea;
  outline: none;
  box-shadow: 0 0 5px rgba(102, 126, 234, 0.5);
}

/* Botón */
button {
  width: 100%;
  padding: 12px;
  border: none;
  border-radius: 8px;
  background: green;
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: 0.3s;
}

/* Hover botón */
button:hover {
  background: #5a67d8;
}



</style>

