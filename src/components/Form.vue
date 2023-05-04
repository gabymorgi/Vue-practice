<script setup lang="ts">
  import { defineProps, ref } from 'vue'
  const emit = defineEmits(['submit'])

  const inputValue = ref('')

  function onSubmit() {
    console.log('submit')
    console.log(inputValue.value)
    emit('submit', inputValue.value)
  }
</script>

<template>
  <form v-on:submit.prevent="onSubmit">
    <label for="input">Github Name:</label>
    <input id="input" v-model="inputValue" />
    <button type="submit">Submit</button>
  </form>
</template>