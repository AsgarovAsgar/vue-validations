<script setup>
import { ref } from 'vue';

const form = ref({
  name: '',
  age: ''
})

function submitForm() {
  const nameIsValid = !!form.value.name
  const ageIsValid = !!form.value.age

  const formIsValid = nameIsValid && ageIsValid
  if(formIsValid) {
    console.log('Submitted', form.value);
  } else {
    console.log('invalid form');
  }
}

</script>

<template>
  <div>
    <form @submit.prevent="submitForm" class="mt-4 p-4 border inline-flex flex-col gap-4">
      <div class="flex flex-col">
        <label for="name">Name:</label>
        <input type="text" v-model="form.name" id="name">
      </div>
      
      <div>
        <label for="age">Age:</label>
        <input type="text" v-model="form.age" id="age">
      </div>

      <div>
        <button type="submit">Submit</button>
      </div>
    </form>
  </div>
</template>