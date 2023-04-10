<template>
    <!-- start of Add Contact Form field -->
    <div class="fixed z-10 inset-0 overflow-y-auto">
        <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
          <div class="fixed inset-0 transition-opacity" aria-hidden="true">
            <div class="absolute inset-0 bg-gray-500 opacity-75"></div>
          </div>
    
          <div class="inline-block align-bottom bg-white rounded-lg text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full">
            <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
              <form class="w-full max-w-sm">
                <div class="md:flex md:items-center mb-6">
                  <div class="md:w-1/3">
                    <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="inline-name">
                     Name
                    </label>
                  </div>
                  <div class="md:w-2/3">
                    <input class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500" id="inline-name" type="text"  v-model="addContactForm.name" required>
                  </div>
                </div>
                <div class="md:flex md:items-center mb-6">
                  <div class="md:w-1/3">
                    <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="inline-phone">
                     Phone
                    </label>
                    </div>
                    <div class="md:w-2/3">
                      <input class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500" id="inline-phone" type="tel" v-model="addContactForm.phone" required>
                    </div>
                </div>
               
                <div class="md:flex md:items-center mb-6">
                    <div class="md:w-1/3">
                      <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="inline-type">
                       Country
                      </label>
                      </div>
                      <div class="md:w-2/3">
                      <select  class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-purple-500" v-model="addContactForm.country"  required>
                        <option value="india">India</option>
                        <option value="canada">Canada</option>
                        <option value="europe">Europe</option>
                        <option value="china">China</option>
                    
                      </select>
                    </div>
                  </div>
        
              </form>
            </div>
            <!-- start of save and contact button -->
            <div class="bg-gray-50 px-4 py-3 sm:px-6 sm:flex sm:flex-row-reverse">
              <button type="button" class="w-full inline-flex justify-center rounded-md border border-transparent shadow-sm px-4 py-2 bg-green-600 text-base font-medium text-white hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-green-500 sm:ml-3 sm:w-auto sm:text-sm" @click="saveContact">
                Save
              </button>
              <button type="button" class="mt-3 w-full inline-flex justify-center rounded-md border border-gray-300 shadow-sm px-4 py-2 bg-white text-base font-medium text-gray-700 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 sm:mt-0 sm:ml-3 sm:w-auto sm:text-sm" @click="cancelcontact">
                Cancel
              </button>
            </div>
             <!-- End of save and contact button -->
          </div>
        </div>
      </div>
     <!-- End of Add Contact Form field -->
</template>
<script setup lang="ts">

  //Defining the schema of reactive ContactForm
  interface ContactForm {
  name:string,
  phone:number,
  country:string
  
}
//Declaring in the empty form and use it in v-model
  let addContactForm:ContactForm=reactive({
   name:'',
   phone:0,
   country:''
  })
//Define the emits
const emits = defineEmits(['cancel','save']);
 //Emitting the cancel  and pass it in main
 const cancelcontact=()=>{
  emits('cancel')
  }

    //Emitting the save and pass it in the main and resetting the value
    const saveContact=()=>{
  console.log("add",addContactForm)
    emits('save',addContactForm)
    addContactForm.name=''
    addContactForm.phone=0
    addContactForm.country=''
  }
</script>