<script setup>
import { ref } from "vue";

const emit = defineEmits(["formSubmit"]);
const searchInput = ref("");

function handleSubmit(ev) {
  ev.preventDefault();

  emit("formSubmit", searchInput.value);
}
</script>

<template>
  <form @submit="handleSubmit">
    <input type="text" v-model.lazy="searchInput" />
    <button>Carregar Usuário</button>
  </form>
</template>

<style scoped>
input,
button {
  max-width: 20rem;
  padding: 0.5rem;
}
input {
  background-color: #1c1a1d;
  border: 1px solid #f64348;
  border-radius: 0.25rem;
  color: #e5e5e5;
  margin: 1rem 1rem 1rem 0;
}
button {
  background-color: #f64348;
  border: unset;
  border-radius: 0.25rem;
  color: #1c1a1d;
  font-size: 1rem;
  font-weight: 700;
  text-transform: uppercase;
}
button:hover {
  cursor: pointer;
  filter: brightness(0.95);
}
</style>
