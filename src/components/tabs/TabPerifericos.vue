
<template>
  <ListaProductos :productos="productosPerifericos" />
</template>

<script setup>
import {computed, onMounted, onUnmounted, onActivated, onDeactivated} from 'vue'
import { productos } from '../../data/productos'
import ListaProductos from '../ListaProductos.vue'

const productosPerifericos = computed(() =>
  productos.filter(
    p => p.categoria === 'Periféricos'
  )
)

onMounted(() => console.log('TabPerifericos - montado'))
onUnmounted(() => console.log('TabPerifericos - desmontado'))
onActivated(() => console.log('TabPerifericos - activado'))
onDeactivated(() => console.log('TabPerifericos - desactivado'))
</script>

