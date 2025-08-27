<script setup>
import { defineProps, defineEmits, ref } from 'vue';

defineProps({
  predictedCargo: {
    type: String,
    required: true
  }
});

defineEmits(['close', 'back']);

// Variável para controlar qual conteúdo exibir na modal
const showInfo = ref(false);

const cargosInfo = {
  'Analista de Dados/Data Analyst': 'Extrai insights de dados existentes. Ele limpa, visualiza e interpreta dados.',
  'Cientista de Dados/Data Scientist': 'Cria modelos preditivos que resolvem problemas complexos. Pesquisa e constrói modelos.',
  'Engenheiro de Dados/Data Engineer': 'Constrói e mantém a infraestrutura que suporta analistas e cientistas de dados.',
  'Outros': 'Abrange cargos que não têm relação direta com a área de Data Science.'
};
</script>

<template>
  <div class="modal-overlay" @click.self="$emit('close')">
    <div class="card modal-card">

      <div class="button-far-left">
        <button class="close-button" @click="$emit('close')">X</button>
      </div>

      <div v-if="!showInfo">
        <header class="modal-header">
          <h2 class="text-gradient">Resultado da Predição</h2>
        </header>
        
        <div class="modal-content">
          <div class="icon-section">
            <p class="celebration-icon">🎉</p>
          </div>
          <p class="prediction-text">
            O cargo mais provável para você é:
            <span class="predicted-cargo">{{ predictedCargo }}</span>
          </p>
          
          <div class="info-section">
            <p>Não entendeu sua resposta? Clique em Saiba mais:</p>
            <button class="card-button-secondary" @click="showInfo = true">
              Saiba mais
            </button>
          </div>
        </div>

        <div class="form-actions">
          <button class="card-button-secondary" @click="$emit('back')">
            Voltar ao formulário
          </button>
        </div>
      </div>

      <div v-else>
        <header class="modal-header">
          <h2 class="text-gradient">Entenda sua Classificação</h2>
        </header>
        
        <div class="modal-content">
          <ul class="cargo-list">
            <li v-for="(description, cargo) in cargosInfo" :key="cargo">
              <strong class="text-gradient">{{ cargo }}</strong>: {{ description }}
            </li>
          </ul>
        </div>
        
        <div class="form-actions">
          <button class="card-button-secondary" @click="showInfo = false">
            Voltar
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.icon-section {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 2%;
}

.modal-card {
  position: relative;
  padding: 2rem;
  min-width: 450px;
  max-width: 700px;
  max-height: 80vh;
  overflow-y: auto;
  text-align: center;
}

.modal-header {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

.close-button {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  display: flex;
}

.modal-content {
  margin-bottom: 20px;
}

.prediction-text {
  font-size: 1.25rem;
  color: var(--color-primary);
}

.predicted-cargo {
  display: block;
  font-size: 1.75rem;
  font-weight: 700;
  color: var(--color-link);
  margin-top: 0.5rem;
  margin-bottom: 1.5rem;
}

.form-actions {
  margin-top: 20px;
  text-align: center;
}

.button-far-left {
  display: flex;
  justify-content: flex-end;
}

.celebration-icon {
  font-size: 3rem;
  margin: 1rem 0;
  display: flex;
}

.info-section {
  margin-top: 20px;
}

.info-section p {
  margin-bottom: 10px;
}

.cargo-list {
  text-align: left;
  list-style-type: none;
  padding: 0;
  margin-top: 20px;
}

.cargo-list li {
  margin-bottom: 15px;
  line-height: 1.4;
}

/* Reajuste para o botão secundário para não atrapalhar a estilização existente */
.card-button-secondary {
  color: var(--color-link) !important;
  background: transparent !important;
  border: 1px solid var(--color-link) !important;
  padding: 0.75rem 1.5rem;
  border-radius: 6px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.card-button-secondary:hover {
  background-color: rgba(100, 255, 218, 0.1) !important;
  color: #fff !important;
}

.text-gradient {
  background: linear-gradient(90deg, #64ffda, #4ade80);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
</style>