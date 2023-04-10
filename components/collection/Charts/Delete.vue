<template>
    <!-- start of delete -->
    <div class="px-6 pt-4 pb-2">
        <button id="deletechart" @click="emitDeleteContact">
        <TrashIcon  class="h-6 w-6"/>
    </button>
      </div>
      <!-- end of delete -->
</template>
<script setup lang="ts">
// importing the trashicon
import { TrashIcon } from "@heroicons/vue/24/outline"
const emits = defineEmits(['delete']);
//  Emitting the Delete to the list
const  emitDeleteContact=()=>{
emits('delete')
}
</script>