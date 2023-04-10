<template>
    <!-- showing the person list starts here -->
    <div class="flex flex-wrap justify-center">

        <div class="flex flex-col bg-white rounded-lg shadow-md w-full m-6 overflow-hidden sm:w-52" v-for="person in personList" :key="person">
            <img :src="'https://www.countryflags.com/wp-content/uploads/' + person.country + '-flag-png-large.png'"   alt="" class="h-20 m-6">
            <h2 class="text-center px-2 pb-5">{{person.name}}</h2>  
            <p class="text-center px-2 pb-5">{{person.phone}}</p>  
            <div class="px-6 pt-4 pb-2">
                <button class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2" @click="deleteContact(person)">Delete</button>
              </div>
        </div>
    </div>
     <!-- showing the person list ends here -->
</template>
<script setup lang="ts">
//Defining the schema of Personschema
interface PersonSchema{
  name:string,
  phone:number,
  gl:string,
  country:string
}
// Getting the props of PersonList
let props = defineProps<{ personList:PersonSchema }>()
const emits = defineEmits(['edit','delete']);
//Emitting the delete and pass it in the main
const deleteContact=(person:any)=>{
    emits('delete',person)
  
}
</script>