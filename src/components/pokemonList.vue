<script setup>
import TaskItem from "@/components/TaskItem.vue";
import PokemonCard from "@/components/pokemonCard.vue";
import { defineProps, ref, onMounted, watch, defineEmits } from "vue";

const props = defineProps({
    pokemonList: { type: Array, required: true },
});

const data = ref([]);
const isLoading = ref(false);

const emit = defineEmits(["remove:pokemon"]);

const del = (index) => {
    emit("remove:pokemon", index);
};

const getData = async () => {
    isLoading.value = true;

    for (const element of props.pokemonList) {
        console.log(element.title);
        const fetched = await fetch(`https://tyradex.vercel.app/api/v1/pokemon/${element.title}`);
        const fetchedData = await fetched.json();
        data.value.push({ index: props.pokemonList.indexOf(element), moreInfo: false, pokemon: fetchedData });
    }
    isLoading.value = false;
};

watch(props.pokemonList, async () => {
    data.value = [];
    await getData();
});

onMounted(async () => {
    await getData();
});

// update pokemon list moreInfo
const updateMoreInfo = (index) => {
    data.value[index].moreInfo = !data.value[index].moreInfo;
};
</script>

<template>
    <div class="listContainer">
        <div v-if="isLoading" class="loading">LOADING</div>
        <div v-else class="grid">
            <div v-for="item in data" :key="item.pokedex_id" class="grid-item">
                <div v-if="!item.moreInfo">
                    <TaskItem @remove:pokemon="del" @update:moreInfo="updateMoreInfo" :pokemon="item" />
                </div>
                <div v-else>
                    <PokemonCard @update:moreInfo="updateMoreInfo" :pokemon="item" />
                </div>
            </div>
        </div>
    </div>
</template>


<style scoped>
.listContainer {
    padding: 20px;
    background: #f9f9f9;
    /* Light background for contrast */
    border-radius: 10px;
    /* Rounded edges for the container */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    /* Subtle shadow for better visuals */
}

.loading {
    text-align: center;
    font-size: 18px;
    font-weight: bold;
    color: #555;
    margin-top: 20px;
}

/* Grid layout for items */
.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    /* Responsive columns */
    gap: 20px;
    /* Space between items */
    margin-top: 20px;
}


/* Responsive design for smaller screens */
@media (max-width: 768px) {
    .listContainer {
        padding: 15px;
    }
}
</style>
