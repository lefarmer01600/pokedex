<script setup>
import { ref } from "vue";
import { defineEmits } from "vue";

const emit = defineEmits(["add"]);

const title = ref("");

const handleAdd = () => {
    if (title.value === "") {
        return;
    }

    const newTask = {
        title: title.value,
    };

    emit("add", newTask);

    title.value = "";
};
</script>

<template>
    <div>
        <input type="text" v-model="title" placeholder="Nom du pokemon ou id" />
        <button @click.prevent="handleAdd">Ajouter</button>
    </div>
</template>

<style scoped>
/* Form container */
div {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    /* Add spacing between input and button */
    margin: 20px 0;
}

/* Input field styling */
input {
    padding: 10px;
    border: 2px solid #3498db;
    /* Blue border */
    border-radius: 5px;
    font-size: 16px;
    width: 100%;
    max-width: 300px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    /* Subtle shadow */
    outline: none;
    transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

input:focus {
    border-color: #217dbb;
    /* Darker blue on focus */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    /* Enhanced shadow on focus */
}

input::placeholder {
    color: #aaa;
    /* Lighter color for placeholder text */
    font-style: italic;
}

/* Button styling */
button {
    padding: 10px 15px;
    font-size: 16px;
    font-weight: bold;
    color: #fff;
    background-color: #3498db;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.2s ease;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

button:hover {
    background-color: #217dbb;
    /* Darker blue on hover */
    transform: translateY(-2px);
    /* Slight lift effect */
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
}

button:active {
    transform: translateY(0);
    /* Reset transform on click */
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

/* Responsive design for smaller screens */
@media (max-width: 480px) {
    div {
        flex-direction: column;
        /* Stack input and button vertically */
        gap: 15px;
    }

    input {
        width: 100%;
        /* Take full width on smaller screens */
    }

    button {
        width: 100%;
        /* Match input width */
    }
}
</style>
