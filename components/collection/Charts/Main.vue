<template>
    <div>
        <div class="p-[50px] flex divide-y-2 border-y">
             <!-- search starts here -->
            <div class="relative mb-4 flex flex-wrap items-stretch">
                <input
                  type="search"
                  class="relative m-0 -mr-px block w-[1%] min-w-0 flex-auto rounded-l border border-solid border-neutral-300 bg-transparent bg-clip-padding px-3 py-1.5 text-base font-normal text-neutral-700 outline-none transition duration-300 ease-in-out focus:border-primary-600 focus:text-neutral-700 focus:shadow-te-primary focus:outline-none dark:border-neutral-600 dark:text-neutral-200 dark:placeholder:text-neutral-200"
                  placeholder="Search"
                  aria-label="Search"
                  aria-describedby="button-addon3"
                  v-model.trim="searchQuery"/>
            
                <!--Search button-->
                <button
                  class="relative z-[2] rounded-r border-2 border-primary px-6 py-2 text-xs font-medium uppercase text-primary transition duration-150 ease-in-out hover:bg-black hover:bg-opacity-5 focus:outline-none focus:ring-0"
                  type="button"
                  id="button-addon3"
                  data-te-ripple-init>
                  Search
                </button>
              </div>
               <!-- search ends here -->
            <!-- start of add button -->
            <div class="ml-[56rem]">
                <button class="flex bg-slate-100" @click="openContact">
                <PlusIcon class="h-6 w-6"/>
                <p class="ml-3">Add Contact</p>
                </button>
            </div>
             <!-- end of add button -->
    <!-- opening the Contact modal by clicking add contact -->
    <CollectionChartsAdd v-show="isContact" @cancel="isContact=false"  @save="saveCountry"/>
       </div>
        <!-- showing person list starts here -->
       <div class="text-center" v-if="!isContact">
        <h1 class="text-3xl">Person List</h1>
         <div>
            <CollectionChartsList :personList="filteredList" @delete="deleteContactListener"/>
        </div>
      </div>
        <!-- showing person list ends here -->
    </div> 
</template>
<script setup lang="ts">
//importing the HeroIcon  and json data
import { PlusIcon } from "@heroicons/vue/24/outline"
import PersonList from  "../../../json/data.json"
//Declaring the personlist,isContact and searchQuery
const personlist=ref(PersonList)
const isContact=ref(false)
const searchQuery = ref("");
////opening the  Add contact model
const openContact=()=>{
    isContact.value=!isContact.value
}
//Adding the existing data in localstorage
onMounted(() => {
const contactData = localStorage.getItem('contact')

  if (contactData) {
    personlist.value = JSON.parse(contactData)
  } else {
    localStorage.setItem('contact', JSON.stringify(personlist.value))
  }
})
//saving the newdata in localstorage
const saveCountry=(addContactForm)=>{
    console.log("addContactForm",addContactForm)
    personlist.value.push(addContactForm)
    const storedContacts = JSON.parse(localStorage.getItem('contact'));
  storedContacts.push(addContactForm);
  localStorage.setItem('contact', JSON.stringify(storedContacts));

}

//Deleting the contact data from localstorage

const deleteContactListener=(person)=>{
    if(confirm('Are you sure to delete this record?')){
    let personIndex=personlist.value.findIndex(item => item.name === person.name)
    if(personIndex!==-1){
        personlist.value.splice(personIndex,1)
        const deletedContacts = JSON.parse(localStorage.getItem('contact'));
        deletedContacts.splice(personIndex,1)
        localStorage.setItem('contact', JSON.stringify(deletedContacts));
    }
}
}
//search the value
const filteredList = computed(() => {
  return personlist.value.filter(
    (person) =>
      person.name.toLowerCase().includes(searchQuery.value.toLowerCase()) 
  );
});



</script>