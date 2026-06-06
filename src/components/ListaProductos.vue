
<template>
  <div v-if="cargando">
    Cargando...
  </div>

  <div
    ref="box"
    class="lista"
    style="max-height:300px; overflow-y:auto; padding-right:10px;"
  >
    <template
      v-for="(producto, index) in props.productos"
      :key="producto.id"
    >

      <TarjetaProducto v-if="index % 3 === 0">
        <template #header>
          <h3>{{ producto.nombre }}</h3>
          <p>{{ producto.categoria }}</p>
        </template>

        <template #body="{ expandida, toggleExpandir }">
          <p>Precio: <strong>${{ producto.precio }}</strong></p>

          <button @click="toggleExpandir">
            {{ expandida ? 'Ocultar' : 'Ver stock' }}
          </button>

          <p v-if="expandida">
            Stock: {{ producto.stock }}
          </p>
        </template>

        <template #footer>
          <button>Comprar</button>
        </template>
      </TarjetaProducto>

      <TarjetaProducto v-else-if="index % 3 === 1">
        <template #header>
          <h3>{{ producto.nombre }}</h3>
          <p>{{ producto.categoria }}</p>
        </template>

        <template #body="{ expandida, toggleExpandir }">
          <p>Precio: <strong>${{ producto.precio }}</strong></p>

          <button @click="toggleExpandir">
            {{ expandida ? 'Ocultar' : 'Ver stock' }}
          </button>

          <p v-if="expandida">
            Stock disponible: {{ producto.stock }}
          </p>
        </template>
      </TarjetaProducto>

      <TarjetaProducto v-else>
        <template #header>
          <h3>{{ producto.nombre }}</h3>
          <p>Categoría: {{ producto.categoria }}</p>
        </template>

        <template #body="{ expandida, toggleExpandir }">
          <p>Precio final: <strong>${{ producto.precio }}</strong></p>

          <button @click="toggleExpandir">
            {{ expandida ? 'Mostrar menos' : 'Ver detalle' }}
          </button>

          <p v-if="expandida">
            Stock disponible: {{ producto.stock }}
          </p>
        </template>

        <template #footer>
          <a href="#">Ver más información</a>
        </template>
      </TarjetaProducto>
    </template>
  </div>
</template>

<script setup>
import { ref, onMounted, onUpdated, onBeforeUnmount, useTemplateRef } from 'vue'
import TarjetaProducto from './TarjetaProducto.vue'

const props = defineProps({
  productos: {
    type: Array,
    required: true
  }
})

const cargando = ref(false)
const box = useTemplateRef('box')

let timer = null

function esperar(ms) {
  return new Promise(resolve => setTimeout(resolve, ms))
}

async function cargarProductos() {
  cargando.value = true
  await esperar(800)
  cargando.value = false
}

onMounted(() => {
  cargarProductos()

  timer = setInterval(() => {
    cargarProductos()
  }, 30000)
})

onUpdated(() => {
  if (box.value) {
    box.value.scrollTop = box.value.scrollHeight
  }
})

onBeforeUnmount(() => {
  clearInterval(timer)
  console.log('ListaProductos desmontado — polling detenido')
})
</script>