<template>
 hi
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute()
const id = route.params.id
const character = ref()


const loadCharacters = async () => {
  const response = await fetch(`https://rickandmortyapi.com/api/character/${id}`)
  const data = await response.json()
  console.log(data)
  characters.value = data
  console.log(character.value)
}

onMounted(()=>{
    loadCharacters()
})
</script>