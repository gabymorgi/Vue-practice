<script setup lang="ts">
  import Card from './Card.vue';
  import { ref, onMounted, watch } from 'vue';

  const repos = ref()
  const loading = ref(false)
  const error = ref('')

  const props = defineProps<{
    user?: string
  }>()

  watch(() => props.user, (newVal) => {
    if (newVal) {
      fetchRepos(newVal)
    }
  })

  async function fetchRepos(userName: string) {
    loading.value = true
    console.log(userName)
    try {
      const data = await (await fetch(`https://api.github.com/users/${userName}/repos`)).json()
      if (data.message === 'Not Found') {
        error.value = 'Este usuario no existe'
        return
      }
      console.log(data)
      repos.value = data
    } catch (error: any) {
      console.log(error)
      error.value = error.message
    } finally {
      loading.value = false
    }
  }

  onMounted(() => {
    if (props.user) {
      fetchRepos(props.user)
    }
  })
</script>

<template>
  <div v-if="repos" class="list">
    <Card :title="repo.name" v-for="repo in repos">
      <p>{{ repo.description}}</p>
    </Card>
  </div>
  <div v-else-if="loading">Loading...</div>
  <div v-else-if="user">Este usuarion no tiene repos publicos</div>
  <div v-else>Selecciona un usuario</div>
  <div v-if="error">{{ error }}</div>
</template>

<style scoped>
  .list {
    padding: 1rem;
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
  }
  .list > * {
    /* three columns */
    width: calc(100% / 3 - 1rem);
  }
</style>