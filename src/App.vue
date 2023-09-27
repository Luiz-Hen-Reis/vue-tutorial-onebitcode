<script setup>
import { ref } from "vue";
import Profile from "./components/Profile.vue";

const isOpen = ref(true);
</script>

<template>
  <input type="checkbox" v-model="isOpen" />
  <Profile v-if="isOpen"
    >Github User Data
    <template v-slot:footer>Desenvolvido por Luiz-Hen-Reis</template>
  </Profile>
</template>

<style>
#app {
  font-family: "Ubuntu", sans-serif;
  min-height: 100vh;
  max-width: 40rem;
  margin: 0 auto;
  text-align: center;
}
</style>
