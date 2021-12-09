<script setup>
    import { onUnmounted, ref } from "vue"
    import useDB from "../composable/useDB"
    import useAuth from "../composable/useAuth"
    
    const  {inventory, unsubscribe, sendSerial, sendBrand} = useDB()
    const {user} = useAuth()
    const newSer = ref('')
    const newBrand = ref('')

    const newSerial = ()  => {
       sendSerial(newSer.value)
       newSer.value =""
    }
    const inputBrand = ()  => {
        sendBrand(newBrand.value)
        newBrand.value= ""
    }
   

      const sendInfo = ()  => {
        newSerial()
        inputBrand()
        inputModel()
       
      }
   

    onUnmounted(() => {
        unsubscribe()
    })
</script>


<template>

<h1 class="mt-5 text-3xl font-medium tracking-wide text-center">Inventory </h1>

<div class="min-h-[600px] w-full mt-6 rounded-lg shadow-md flex flex-col justify-between bg-blue-400">

    
<table v-for="invent in inventory" :key="invent.id">
    <tr class="text-sm rounded-sm">
        <th>SERIAL NUMBER</th>
        <th>MANUFACTUER</th>
       
    </tr>
    <tr class="text-lg font-thin text-center bg-gray-100 rounded-md">
        <td>{{invent.serial}}</td>
        <td>{{invent.brand}}</td>
        
        
    </tr>

</table>


    <div class="flex justify-center">
        <input class="p-4 rounded-lg focus:outline-none focus:bg-red-300" type="text" placeholder="Type a serial!!!!" 
        v-model="newSer"  >
         <input class="p-4 rounded-lg focus:outline-none focus:bg-red-300" type="text" placeholder="Type a brand!!!!" 
        v-model="newBrand">
       
        <button class="p-2 bg-gray-400 rounded-md focus: hover:bg-green-400" @click="sendInfo">Add Unit</button>
        
    </div>

</div>

</template>