<template>
  <div v-if="loading">Loading...</div>

  <div v-else-if="error">Error: {{ error.message }}</div>
  <ul v-else-if="result.characters.results">
    <li v-for="user of result.characters.results" :key="user.id">
      {{ user.id}} ------------------------ {{ user.name }} --------------------- {{ user.image }}
    </li>
  </ul>
</template>

<script>
import { useQuery } from '@vue/apollo-composable'
import gql from 'graphql-tag'

export default {
  setup () {
    const { result, loading, error } = useQuery(gql`
    query Characters {
      characters {
        results{
          id
          name
          image
        }
      }
    }  
  `)
    return {
      result,
      loading,
      error,
    }
  },
}
</script>
