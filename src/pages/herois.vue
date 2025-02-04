<script>
import axios from 'axios';

export default {
  async mounted() {
    console.log('Making request to:', 'http://localhost:3003/characters'); // Verifique se a URL está correta
    console.log('Component mounted, making request...'); // Verifique se isso aparece no console

    try {
      const response = await axios.get('http://localhost:3003/characters');
      console.log('response : ',response.data);
      console.log('requisição para : ', response); 
      this.characters = response.data; // Store data in component state
    } catch (error) {
      console.log('Error fetching characters:', error);
      // Handle errors gracefully (e.g., display an error message)
    }
  },
  data() {
    return {
      characters: [], // Initialize empty array for characters
    };
  },
};
</script>

<template>
  <div v-if="characters.length">
    <h2>Marvel Characters</h2>
    <ul>
      <li v-for="character in characters" :key="character.id">
        {{ character.name }}
      </li>
    </ul>
  </div>
  <div v-else>
    Loading characters...
  </div>
</template>