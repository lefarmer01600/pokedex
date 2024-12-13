
<script setup>
import { defineProps , defineEmits } from "vue";

const emit = defineEmits(["update:moreInfo"]);

const props = defineProps({
  pokemon: { type: Object, required: true },
});

const deletePokemon = () => {
  emit("remove:pokemon", props.pokemon.index);
};

const handleMoreInfo = () => {
  emit("update:moreInfo", props.pokemon.index);
};


</script>

<template>
    <div class="item">
        <img :src="pokemon.pokemon.sprites.regular" alt="pokemon" />
        <p>{{ pokemon.pokemon.name.fr }}</p>
        <button @click.prevent="deletePokemon">Suprimer</button>
        <button @click.prevent="handleMoreInfo" >Detail</button>
    </div>
</template>

<style scoped>
.item {
  padding: 20px;
  border-radius: 15px;
  border: 2px solid #3498db; /* Softer blue */
  background: linear-gradient(135deg, #f0f9ff, #d6eaff);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 300px;
  margin: 20px auto; /* Center alignment */
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.item:hover {
  transform: translateY(-5px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
}

.item p {
  margin: 5px 0;
  font-size: 14px;
  color: #333;
  line-height: 1.5;
  font-weight: 500; /* Medium weight for better readability */
}

.item p:first-of-type {
  font-weight: 700; /* Name highlighted */
  font-size: 16px;
}

img {
  width: 100%;
  border-radius: 15px;
  margin-bottom: 10px;
  border: 1px solid #ccc; /* Light border around the image */
  background-color: #fff;
}

button {
  margin-top: 15px;
  padding: 10px 15px;
  margin-right: 10px;
  font-size: 14px;
  font-weight: 600;
  color: #fff;
  background-color: #3498db;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

button:hover {
  background-color: #217dbb; /* Darker blue on hover */
}

@media (max-width: 768px) {
  .item {
    max-width: 90%;
  }
}

</style>
