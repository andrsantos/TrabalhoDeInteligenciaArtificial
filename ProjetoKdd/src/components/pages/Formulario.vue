<script setup>
import { ref } from 'vue';
import ModalForm from './ModalForm.vue';
const showModal = ref(false);
</script>

<template>
  <div class="welcome-container">
    <div class="card">
      <h1>Projeto de predição de cargos com Machine Learning</h1>
      <p>
        Teste nossa plataforma para descobrir o cargo ideal para você com base em suas habilidades e preferências.
      </p>
      <button class="card-button-primary" @click="showModal = true">Explorar a Plataforma</button>
    </div>
  </div>
    <ModalForm v-if="showModal" @close="showModal = false" />
</template>

<style scoped>
/* Estilos específicos do componente */
.welcome-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 20px;
}

/* O card e os elementos internos serão estilizados pelo fanta.css */
.card {
  text-align: center;
  max-width: 500px;
  width: 100%;
}
</style>
