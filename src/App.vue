<template>
<h2>Cena {{ contador }}
con el rey godo {{ rey }}
</h2>
<h3 class="precio"> Precio: {{ productos[contador].precio }}$ </h3>
<div v-if="productos[contador].finDeSemana" class="soloFinesDeSemana dias">(Solo fines de semana)</div>
<div v-else class="dias todosLosDias">(Solo fines de semana)</div>
<div v-if="productos[contador].precio<100" class="oferta">
    <div>Ahora un 10 % descuento:
        {{ nuevoPrecio }}$
    </div>
    <img src="/src/assets/tag.svg" alt="rey godo en descuento" class="ofertaTag" />
    <!-- <svg-icon type="mdi" :path="path"></svg-icon> -->
</div>

<img :src="imagen" alt=""/>
<button @:click="siguiente">Siguiente ({{ contador + 1 }}/{{total}} )</button>
</template>

<script setup>
import {ref,computed } from "vue"
import {productos} from "./datos" 

const contador = ref(0)
const total = productos.length;
//https://www.html6.es/img
//const ruta = "https://www.html6.es/img/rey_"
const ruta = "https://images.pexels.com/photos/"
const subruta = "/pexels-photo-"
//https://images.pexels.com/photos/3573351/pexels-photo-3573351.png   

const siguiente=()=>{
    contador.value++
    if(contador.value>=total){
        contador.value=0
    }
}
const rey=computed(()=>{
    const elNombre=productos[contador.value].nombre.toLowerCase()
    return elNombre.substring(0,1).toUpperCase() + elNombre.substring(1)
})
const imagen=computed(()=>{
    return `${ruta}${productos[contador.value].nombre.toLocaleLowerCase()}${subruta}${productos[contador.value].nombre.toLocaleLowerCase()}.png?auto=compress&cs=tinysrgb&dpr=1&fit=crop&h=200&w=280`
})
const nuevoPrecio=computed(()=>{
    return Number(productos[contador.value].precio/1.10).toFixed(2)
})

</script>

<style scoped>

.todosLosDias{
    background-color: green;
}

.soloFinesDeSemana{
    background-color: red;
}


</style>