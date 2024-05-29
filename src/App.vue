<template>
  <div>
    <div class="top">
      <h1>Rick and Morty Characters</h1>
    </div>
    <div>
      <input v-model="filters.name" placeholder="Name">
      <select v-model="filters.status">
        <option value="">Any Status</option>
        <option value="alive">Alive</option>
        <option value="dead">Dead</option>
        <option value="unknown">Unknown</option>
      </select>
      <button @click="applyFilters">Apply</button>
    </div>
    <div class="cards-container">
      <CharacterCard
        v-for="character in characters"
        :key="character.id"
        :character="character"
      />
    </div>
    <div>
      <button @click="changePage(-1)" :disabled="!prev">Prev</button>
      <button @click="changePage(1)" :disabled="!next">Next</button>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, watchEffect } from 'vue';
import CharacterCard from './components/CharacterCard.vue';

const apiUrl = 'https://rickandmortyapi.com/api/character';
const characters = ref([]);
const prev = ref(null);
const next = ref(null);

const filters = reactive({
  name: '',
  status: ''
});

const fetchData = async () => {
  let url = `${apiUrl}?name=${filters.name}&status=${filters.status}`;
  const response = await fetch(url);
  const data = await response.json();
  characters.value = data.results;
  prev.value = data.info.prev;
  next.value = data.info.next;
};

watchEffect(() => {
  fetchData();
});

const applyFilters = () => {
  fetchData();
};

const changePage = async (direction) => {
  const pageUrl = direction === 1 ? next.value : prev.value;
  if (pageUrl) {
    const response = await fetch(pageUrl);
    const data = await response.json();
    characters.value = data.results;
    prev.value = data.info.prev;
    next.value = data.info.next;
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Rubik:ital,wght@0,300..900;1,300..900&display=swap');

body {
  background-color: rgb(39, 43, 51);
  font-family: "Rubik", sans-serif;
  font-optical-sizing: auto;
  font-weight: 500;
  font-style: normal;
  margin: 0px !important;
}

.top {
  background: white;
  text-align: center;
  height: 80px;
  display: flex;
  justify-content: center;
  align-items: center;
}

h1 {
  margin: 0px;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 20px;
  
  margin: 20px;
}

button {
  margin: 10px;
  padding: 10px 20px;
  background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
}

button:disabled {
  background-color: #a5a5a5;
}

input, select {
  margin: 10px;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}
</style>

