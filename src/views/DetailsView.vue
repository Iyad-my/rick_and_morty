<template>
  <div class="flex justfy-center items-center h-screen">
  <div class="grid grid-cols-1 lg:grid-cols-2 mt-8 lg:w-6xl" v-if="character">
    <div class="flex justify-center">
      <img class="rounded-2xl w-96" :src="character.image" :alt="character.name">
    </div>

    <div class="flex flex-col items-center mx-auto mt-8 shadow-2xl p-4 rounded-2xl w-xl">
      <h1 class="text-3xl font-bold mb-4">{{character.name}}</h1>
      <div class=" lg:space-y-4 text-xl">
      <p><b>Ubicacion:</b>{{character.location.name}}</p>
      <p><b>Origen:</b>{{character.origin.name}}</p>
      <p><b>Estado:</b>{{character.status}}</p>
      <p><b>Especie:</b>{{character.species}}</p>
      <p><b>Genero:</b>{{character.gender}}</p>
    </div>
  </div>
</div>
</div>
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
  character.value = data
  console.log(character.value)
}

onMounted(()=>{
    loadCharacters()
})
</script>