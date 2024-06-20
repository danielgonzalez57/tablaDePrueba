<script setup>
import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios';

const info = ref([]);
const loadingInfo = ref(false);
const baseUrl = `http://localhost:3002/api/orders`;

import { ref, computed, onMounted } from 'vue';

const headers = ref([
  {title: 'COMANDA', key: 'ID_order' },
  {title: 'CEDULA', key: 'Cedula'}, 
  {title: 'SUCURSAL', key: 'Sucursal'}, 
  {title: 'CLIENTE', key: 'Cliente'}, 
  {title: 'FECHA', key: 'Create_date'},
  {title: 'ASESOR', key: 'Asesor'},
  {title: 'STATUS', key: 'Status'},
]);

const boats = ref([
  {
    name: 'Speedster',
    speed: 35,
    length: 22,
    price: 300000,
    year: 2021,
  },
  // ... otros barcos ...
]);

const getOrders = async () => {
    loadingInfo.value = true
    try{
        const url = `${baseUrl}/masterOrder`
        const {data} = await axios.get(url);
        info.value =  data[0]
    } catch(error){
        console.log(error)
    }
    loadingInfo.value = false
}


onMounted( async () => {
    await getOrders();
});
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <div>
    <v-data-table 
        hover 
        density="comfortable"
        v-model:search="search"
        :loading="loadingInfo"
        :items="info"
        :headers="headers"
        :no-data-text="'No hay datos disponibles'"
        :sort-by="ID_order"
        :sort-desc="[true]"
      >

    </v-data-table>
  </div>

</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
