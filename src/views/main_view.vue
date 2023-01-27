<template>
  <div class="header">First Cash</div>

  <n-space class="m-5">
  
    <n-card :title="room.title" v-for="room in rooms" :key="title" class="cards">
      <n-space justify="between-center" class="title1">
          Contador: {{ room.contador }}
      </n-space>
      <n-space justify="between-center">
        <div class="title2">H {{ room.humidity }}</div>
        <div class="title3">|</div>
      <div class="title2">{{ room.temperture }} °</div>
      </n-space>
      <div class="title2 focostop">
        <n-space justify="space-between" class="focos">
         
          <n-icon>
            <bulb-outline v-if="room.foco1='off'"></bulb-outline>
            <bulb v-else></bulb>
            <n-switch></n-switch>
          </n-icon>
          <n-icon>
            <bulb-outline v-if="room.foco2='off'"></bulb-outline>
            <bulb v-else></bulb>
            <n-switch></n-switch>

          </n-icon>
          <n-icon>
            <bulb-outline v-if="room.foco3='off'"></bulb-outline>
            <bulb v-else></bulb>
            <n-switch></n-switch>
          </n-icon>
          <n-icon>
            <bulb-outline v-if="room.foco4='off'"></bulb-outline>
            <bulb v-else></bulb>
            <n-switch></n-switch>
          </n-icon>
          
          <n-icon>
            <bulb-outline v-if="room.foco5='off'"></bulb-outline>
            <bulb v-else></bulb>
            <n-switch></n-switch>
          </n-icon>
          <n-icon>
            <bulb-outline v-if="room.foco6='off'"></bulb-outline>
            <bulb v-else></bulb>
            <n-switch></n-switch>
          </n-icon>
               
        </n-space>
     
        
      </div>
      
    </n-card>
  
</n-space>
</template>
<script setup>
import { ref,reactive,onMounted } from "vue";
import axios from 'axios'
import { BulbOutline,Bulb } from '@vicons/ionicons5'

const mensaje = ref();
const rooms = reactive([])

const refresh= async () => {
  try {
    rooms.splice(0,rooms.length)
    const {data} =await axios({
      method: 'GET',
      url: 'http://localhost:3001/api/getHouses'
    })

    for(const title in data.data)
    {
       const room = {
        title: title,
        temperture: data.data[title]['temperature'],
        humidity: data.data[title]['humidity'],
        foco1: data.data[title]['foco1'],
        foco2: data.data[title]['foco2'],
        foco3: data.data[title]['foco3'],
        foco4: data.data[title]['foco4'],
        foco5: data.data[title]['foco5'],
        foco6: data.data[title]['foco6'],
        foco7: data.data[title]['foco7'],
        contador: data.data[title]['contador'],
       }

       rooms.push(room)

       
    }

    
  } catch (error) {
    console.log(error)
  }
}

onMounted(() => {
  refresh()
  setInterval(refresh,20000)
})

console.log(mensaje);
</script>
<style lang="scss" >


.header{
  background-color: #1d5f3c !important;
  color: #fffefe !important;
  


}

  .title1{
    font-size: 1.3rem;
    font-weight: bolder;
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

   .focos{
    width: 100%;

    div {
      width: 30%;
    };

  }


</style>
