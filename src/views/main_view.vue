<template>
  <div class="header">First Cash</div>

  <n-space class="m-5">
  
    <n-card :title="room.title" v-for="room in rooms" :key="title" class="cards">
      
      <n-space justify="between-center">
        <div class="title2">{{ room.humidity }}</div>
        <div class="title3">|</div>
      <div class="title2">{{ room.temperture }}</div>
      <n-divider vertical title-placement="left">luz</n-divider>
      <div class="title2">
        <n-icon>
          <flash-off v-if="!room.foco1"/>
          <flash v-if="room.foco1"></flash>
        </n-icon>
      </div>
      </n-space>
    </n-card>
  
</n-space>
</template>
<script setup>
import { ref,reactive } from "vue";
import { FlashOff,Flash } from '@vicons/ionicons5'

const mensaje = ref();
const rooms = reactive([])

rooms.push(
  {
    title: 'Casa 1',
    temperture: '23º',
    humidity: '34',
    foco1: false
  }
)

rooms.push(
  {
    title: 'Casa 2',
    temperture: '34º',
    humidity: '23',
    foco1: true
  })
console.log(mensaje);
</script>
<style scoped>
.header{
  background-color: #1d5f3c;
  color: #fffefe !important;
  padding: 1rem;
  margin: 0rem auto 3rem auto;


}

  .title2{
    font-size: 2rem !important;
    font-weight: 900;
  }

  .title3{
    font-size: 2rem; 
    margin-top: -4px;
  }

  .cards{
    background-color:rgb(241, 244, 243);
    margin-bottom: 2rem; 
  }

  .n-card{
    border-radius: 1rem;
  }
  .m-5{
    margin: 2rem;
  }
</style>
