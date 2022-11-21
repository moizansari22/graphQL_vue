<template>
  <p v-if="error">Something went wrong...</p>
  <p v-if="loading">Loading...</p>
  <p v-else v-for="character in result.characters.results" :key="character.id">
    id: {{ character.id}} ---------- Name:{{ character.name }} ------------ images:{{ character.image }}
  </p>
  <div></div>
</template>

<script>
import gql from 'graphql-tag'
import { useQuery } from '@vue/apollo-composable'

const CHARACTERS_QUERY = gql`
  query Characters {
    characters {
      results{
        id
        name
        image
      }
    }
  }
`;
export default {
  name: 'App',
  setup () {
    const { result, loading, error } = useQuery(CHARACTERS_QUERY);
    return {
      result,
      loading, 
      error
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
