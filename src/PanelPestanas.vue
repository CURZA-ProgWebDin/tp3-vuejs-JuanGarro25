
<template>
  <h2>Sin KeepAlive</h2>

  <div class="tabs">
    <button @click="tabNormal = 'todos'">
      Todos
    </button>

    <button @click="tabNormal = 'electronica'">
      Electrónica
    </button>

    <button @click="tabNormal = 'perifericos'">
      Periféricos
    </button>
  </div>

  <component :is="tabs[tabNormal]" />

  <hr class="separador">

  <h2>Con KeepAlive</h2>

  <div class="tabs">
    <button @click="tabKeepAlive = 'todos'">
      Todos
    </button>

    <button @click="tabKeepAlive = 'electronica'">
      Electrónica
    </button>

    <button @click="tabKeepAlive = 'perifericos'">
      Periféricos
    </button>
  </div>

  <KeepAlive>
    <component :is="tabs[tabKeepAlive]" />
  </KeepAlive>

<!--
¿En qué situación conviene usar KeepAlive y en cuál no? 

Conviene usar KeepAlive cuando queremos conservar el estado 
de un componente al cambiar de pestaña.

No conviene usarlo cuando necesitamos que el componente se reinicie 
completamente cada vez que se vuelve a mostrar. 
-->

</template>


<script setup>
import { ref } from 'vue'

import TabTodos from './components/tabs/TabTodos.vue'
import TabElectronica from './components/tabs/TabElectronica.vue'
import TabPerifericos from './components/tabs/TabPerifericos.vue'

const tabs = {
  todos: TabTodos,
  electronica: TabElectronica,
  perifericos: TabPerifericos
}

const tabNormal = ref('todos')
const tabKeepAlive = ref('todos')
</script>