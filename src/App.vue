<script setup lang="ts">
  import { ref } from 'vue';
  import List from './components/List.vue';
  import Form from './components/Form.vue';

  const selectedUser = ref('')

  const handleUserSelected = (user: string, asdf: any) => {
    console.log(user, asdf)
    selectedUser.value = user
  }
</script>

<template>
  <Form @submit="handleUserSelected" />
  <List :user="selectedUser" />
</template>

<style scoped>

</style>
