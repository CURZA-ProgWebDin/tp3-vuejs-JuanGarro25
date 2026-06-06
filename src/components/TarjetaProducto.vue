
<template>
  <div class="tarjeta-producto">
    <div>
      <slot name="header"></slot>
    </div>

    <div>
      <slot
        name="body"
        :expandida="expandida"
        :toggleExpandir="toggleExpandir"
      />
    </div>

    <div class="acciones">
      <slot name="footer">
        <span>Sin acciones disponibles</span>
      </slot>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const expandida = ref(false)

function toggleExpandir() {
  expandida.value = !expandida.value
}
</script>