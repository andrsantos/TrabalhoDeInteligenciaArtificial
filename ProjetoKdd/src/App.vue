<template>
  <div id="app" class="flex-column">
    <header class="app-header">
      <nav class="main-nav">
        <ul class="nav-list">
          <li><a href="#" class="nav-item" @click.prevent="currentPage = 'home'">Página inicial</a></li>
          <li><a href="#" class="nav-item" @click.prevent="currentPage = 'about'">Sobre o projeto</a></li>
          <li>
            <a 
              href="https://t.me/PreditorDeCargosBot" 
              class="nav-item" 
              target="_blank"
              rel="noopener noreferrer"
            >
              Bot no telegram
            </a>
          </li>
        </ul>
      </nav>
    </header>

    <main class="main-content flex-center">
      <div v-if="currentPage === 'home'" class="card">
        <div class="initial-text"><h1 class="text-gradient">Preditor de cargos</h1></div>
        <div class="icon-section"><p class="robot-icon">🤖</p></div>
        
       <div class="description-text"> <p>Olá, bem-vindo ao bot de predição de cargos. Clique em **Comece agora** para iniciar!</p></div>
        <div class="card-actions">
          <button class="card-button-primary" @click="showModal = true">
            Comece agora
          </button>
        </div>
      </div>
      
      <AboutPage v-if="currentPage === 'about'" />
    </main>

    <footer class="app-footer">
      <small>Created by Andrey Santos, Bryan Young e Mayara Lima</small>
    </footer>

    <ModalForm v-if="showModal" 
      @close="showModal = false" 
      @prediction-ready="handlePrediction" 
    />

    <ResultModal v-if="showResultModal"
      :predicted-cargo="predictedCargo"
      @close="showResultModal = false"
      @back="handleBackToForm"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import ModalForm from './components/pages/ModalForm.vue';
import ResultModal from './components/pages/ResultModal.vue';
import AboutPage from './components/pages/AboutPage.vue';

const showModal = ref(false);
const showResultModal = ref(false);
const predictedCargo = ref('');
const currentPage = ref('home');

const handlePrediction = (cargo) => {
  predictedCargo.value = cargo;
  showModal.value = false;
  showResultModal.value = true;
};

const handleBackToForm = () => {
  showResultModal.value = false;
  showModal.value = true;
};
</script>

<style>
@import './fanta.css';

.icon-section{
  display:flex;
  justify-content: center;
  align-items: center;
  margin-bottom:2%;
}

.initial-text{
  display:flex;
  justify-content: center;
  align-items: center;
  margin-bottom:2%;
}

.description-text{
  display:flex;
  justify-content: center;
  align-items: center;
  margin-bottom:2%;
  text-align: center;
  max-width: 400px;
}

:root {
  --background-primary: #121212;
  --background-muted: #1e1e1e;
  --color-primary: #f0f0f0;
  --color-link: #64ffda; /* Cor vibrante para destaque */
  --color-link-transparent: rgba(100, 255, 218, 0.1);
  --border-secondary: #333;
  --border-highlight: #64ffda;
  --border-radius-small: 6px;
}

body {
  background-color: var(--background-primary);
  color: var(--color-primary);
  font-family: Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0;
}

#app {
  width: 100%;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.flex-column {
  display: flex;
  flex-direction: column;
}

/* Estilo para a imagem de fundo */
.main-content {
  flex-grow: 1;
  padding: 20px;
  background-image: url('./assets/ia-background.jpg'); 
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  background-attachment: fixed;
  position: relative;
  
  /* Cria uma camada escura semi-transparente para o texto ficar legível */
  box-shadow: inset 0 0 0 1000px rgba(0,0,0,.7); 
}

/* Estilos para a navegação e o rodapé */
.app-header {
  background-color: var(--background-muted);
  border-bottom: 1px solid var(--border-secondary);
  padding: 1rem 2rem;
  display: flex;
  justify-content: center;
}

.main-nav {
  width: 100%;
  max-width: 900px;
}

.nav-list {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
  justify-content: center;
  gap: 2rem;
}

.nav-item {
  color: var(--color-primary);
  text-decoration: none;
  font-weight: bold;
  font-size: 1rem;
  transition: color 0.3s ease;
}

.nav-item:hover {
  color: var(--color-link);
}

.app-footer {
  background-color: var(--background-muted);
  border-top: 1px solid var(--border-secondary);
  padding: 1rem;
  text-align: center;
  color: #888;
}

.card {
  border: 1px solid var(--border-secondary);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  z-index: 1; /* Garante que o card fique acima do fundo */
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.5);
}

.card-button-primary {
  color: var(--background-primary) !important;
  background: var(--color-link) !important;
}

.card-button-secondary {
    color: var(--color-link) !important;
    background: var(--color-link-transparent) !important;
    border: 1px solid var(--color-link) !important;
}

.card-button-primary:hover, .card-button-secondary:hover {
  opacity: 0.8 !important;
}

.text-gradient {
  background: linear-gradient(90deg, #64ffda, #4ade80);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

/* Novo estilo para o ícone do robô */
.robot-icon {
  font-size: 3rem; 
  text-align: center;
  margin: 1rem 0;
}
</style>