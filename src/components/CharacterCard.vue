<template>
  <div class="card">
    <img :src="character.image" alt="character.name">
    <div>
    <h2>{{ character.name }}</h2>
    <p><span class="prop" style="margin-top: 16px;">Status: </span> {{ character.status }}</p>
    <p><span class="prop">Species:</span> {{ character.species }}</p>
    <p><span class="prop">Gender:</span> {{ character.gender }}</p>
    <!-- Вместо ссылок, выводим текст -->
    <p><span class="prop">Origin:</span> {{ character.origin.name }}</p>
    <p><span class="prop">Last known location:</span> {{ character.location.name }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    character: Object
  }
}
</script>

<style>

.prop {
  color: rgb(158, 158, 158);
  margin-right: 4px;
}
.card {
  display: flex;
  background-color: #3c3e44;
  color: white;
  border-radius: 10px;
  width: 47%;
  height: 207px;
  overflow: hidden;
  margin: 10px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  scale: 1;
  transition-duration: 0.5s;
}

.card:hover {
  scale: 1.04;
}

p, h2 {
  margin: 4px;
}

h2 {
  margin-bottom: 16px;
}

.card img {
  object-fit: cover;
}

.card div {
  padding: 10px;
}
</style>

