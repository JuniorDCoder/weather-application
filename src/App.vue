<script setup>
  import { ref } from 'vue'
  import SearchInput from './components/SearchInput.vue'
  import WeatherCard from './components/WeatherCard.vue'

  const places = ref([])
  const addPlace = (data) => {
    places.value.push(data)
  }

  const deletePlace = (name) => {
    places.value = places.value.filter(place => place.location.name !== name)
  }
</script>

<template>
<main>
  <!-- Date -->
  <div class="text-center mb-6">
    {{ 
      new Date().toLocaleString('en-us', {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      }) 
    }}
  </div>

  <!-- Weather -->
  <div>
    <SearchInput @place-data="addPlace"/>

  </div>

  <!--Weather Cards-->
  <div class="grid grid-cols-2 gap-4">
    <div v-for="(place, idx) in places" :key="idx">
      <WeatherCard :place="place" @delete-place="deletePlace"/>
    </div>
  </div>
</main>
  
</template>