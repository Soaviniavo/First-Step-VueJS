<script setup>
import { ref } from 'vue';
const count  = ref(0);
const movieName = ref("");
const increment = () => {
  count.value++ ; 
}
const decrement = () => {
  count.value-- ; 
}
const delete_movie = (movie) => {
  movies.value = movies.value.filter(m => m != movie );
}
const addMovie = () => {
  movies.value.push(movieName.value);
  movieName.value = ""
}


const movies = ref([
  'Matrix',
   ' Fantastic ',
   'Alice'
]);

</script>

<template>
  <h1>You did it!</h1>
  <p>
     Compteur : {{ count }}
  </p>
  <p v-if="count >=5" :style="{color: count >= 5 ? 'red' : 'green' }" >Vous avez cliqué 5 fois </p>
  <button @click="increment">Incrémenter</button>
  <button @click="decrement">Décrémenter</button>
  
  <ul>
    <li v-for="movie in movies" :key="movie">
      {{ movie }} <button @click="delete_movie(movie)">supp</button>
    </li>
  </ul>
  <form action="" @submit.prevent="addMovie">
   <input type="text" placeholder="Nouveau Film" v-model="movieName">
  <button @click="decrement">Nouveau Film</button>
  </form>
</template>

<style scoped></style>
