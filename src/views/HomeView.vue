<template>
  <main>
    <div class="flex justify-center items-center mt-8">
    <h1 class="text-4xl text-blue-900">
    Rick and Morty
    </h1>
  </div>

  <div class="flex justify-center space-x-4 mt-8">
  <button class="border-2 border-black rounded-full p-1 " @click="decrementPage">-</button>
<div> {{ page }}</div>
<button class="border-2 border-black rounded-full p-1 " @click="incrementPage">+</button>
</div>


  <div class="grid grid-cols-6 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5  gap-7 mt-24 mx-10">
    <div  v-for="character in characters" :key="character.id"  class="rounded-2xl overflow-hidden shadow-2xl">
      <div @click="seeCharacterDetails(character.id)">
      <img :src="character.image" alt="character.name">
      <div class="mt-4 text-center ">
      {{ character.name }}
      </div>
    </div>
    </div> 
    </div>
  </main>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const characters: any = ref([])
const page:any = ref(1)

const loadCharacters = async () => {
  const response = await fetch(`https://rickandmortyapi.com/api/character?page=${page.value}`)
  const data = await response.json()
  characters.value = data.results
}

const incrementPage =()=>{
  page.value++
  loadCharacters()
}

const decrementPage =()=>{
  if(page.value > 1){
    page.value--
 loadCharacters()
  }
}

const seeCharacterDetails =(character_id: number)=>{
  router.push(`/details/${character_id}`)

}



onMounted(() => {
  loadCharacters()
})
</script>


<style>



</style>