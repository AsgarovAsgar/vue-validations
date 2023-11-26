<script setup>
import SimpleForm from '@/components/SimpleForm.vue';
import SimpleFormVuelidate from '@/components/SimpleFormVuelidate.vue';
</script>

<template>
  <main>
    <h1>Home</h1>
    <div class="flex w-full border gap-4">
      <SimpleForm v-if="false"/>
      <SimpleFormVuelidate />
    </div>
  </main>
</template>
