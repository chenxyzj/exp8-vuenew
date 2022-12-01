<script>
import axios from 'axios'
 export default{
   data(){
      return{
        sensors:[
          {id:1, name:"温度传感器"}
        ]
      }
   },
   mounted(){
    this.getSensors()
   },
   methods:{
    async getSensors(){
      const res = await axios.get('https://chenxyzj-glorious-journey-9jqr9wvgrh76r4-8000.preview.app.github.dev/api/sensors')
      //console.log(res);
      this.sensors = res.data;
    },
    async deleteSensor(sensor){
     await axios.delete('https://chenxyzj-glorious-journey-9jqr9wvgrh76r4-8000.preview.app.github.dev/api/sensors/'+sensor.id)
     this.getSensors()
    },
    async addSensor(){
      await axios.post('https://chenxyzj-glorious-journey-9jqr9wvgrh76r4-8000.preview.app.github.dev/api/sensors/',
       {
          name: 'new Sensor'
      })
      this.getSensors()
    }
   }
 }
</script>

<template>
  <button @click="getSensors">Get All sensors</button>
  <button @click="addSensor">Add One Sensor</button>
<ul>
  <li v-for="sensor in sensors" key="sensor.id">
    {{sensor.id}} - {{sensor.name}}
    <button @click="deleteSensor(sensor)">X</button>
  </li>
</ul>
</template>

<style scoped>

</style>
