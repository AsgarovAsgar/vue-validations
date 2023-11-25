<script setup>
import { ref, computed } from 'vue';

const form = ref({
  name: '',
  age: ''
})

const nameIsValid = computed(() => !!form.value.name)
const ageIsValid = computed(() => !!form.value.age)
const formIsValid = computed(() => nameIsValid.value && ageIsValid.value)

function submitForm() {
  if(formIsValid.value) {
    console.log('Submitted', form.value);
  } else {
    console.log('invalid form');
  }
}

</script>

<template>
  <div>
    <form @submit.prevent="submitForm" class="mt-4 p-4 w-full max-w-xl rounded-lg border inline-flex flex-col gap-4">
      <div class="flex flex-col gap-1">
        <label for="name">Name:</label>
        <input class="border rounded px-3 p-1.5" type="text" v-model="form.name" id="name">
        <p v-if="!nameIsValid" class="text-sm text-red-400">Name is required</p>
      </div>
      
      <div class="flex flex-col gap-1">
        <label for="age">Age:</label>
        <input  class="border rounded px-3 p-1.5" type="text" v-model.number="form.age" id="age">
        <p v-if="!ageIsValid" class="text-sm text-red-400">Age is required</p>
      </div>

      <div>
        <button :disabled="!formIsValid" type="submit" class="px-3 py-1.5 w-full border rounded bg-blue-600 text-white disabled:bg-gray-500">Submit</button>
      </div>
    </form>
  </div>
</template>