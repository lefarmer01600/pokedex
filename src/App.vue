<script setup>
import { ref } from "vue";
import TaskList from "@/components/pokemonList.vue";
import TaskForm from "@/components/TaskForm.vue";


const pokemonList = ref([
    {title : "1"},
  ]);

const add = (task) => {
  pokemonList.value.push(task);
};

const del = (index) => {
  pokemonList.value.splice(index, 1);
};
</script>

<template>
  <div class="container">
    <TaskForm @add="add" />
    <TaskList @remove:pokemon="del" :pokemonList="pokemonList" />
  </div>
</template>


<style scoped>
/* Parent container to structure the layout */
.container {
  max-width: 800px; /* Constrain width for better readability */
  margin: 0 auto; /* Center content */
  padding: 20px;
  background: #f4f7fb; /* Subtle background color for contrast */
  border-radius: 10px; /* Rounded corners */
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1); /* Subtle shadow for depth */
}

/* Space between TaskForm and TaskList */
.container > *:not(:last-child) {
  margin-bottom: 20px;
}

/* Responsive design for smaller screens */
@media (max-width: 768px) {
  .container {
    padding: 15px;
  }
}
</style>
