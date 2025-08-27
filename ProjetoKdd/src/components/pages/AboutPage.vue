<template>
  <div class="about-card card">
    <h2 class="text-gradient">Sobre o Projeto de Predição de Cargos</h2>
    <p>
      Este projeto é um trabalho da disciplina de Inteligência Artificial, desenvolvido pelo grupo composto por <strong>Andrey Santos, Mayara Lima e Bryan Young</strong>. Nosso objetivo foi criar uma aplicação que utilizasse um modelo de IA para prever a ocupação profissional de uma pessoa a partir de seu perfil de dados.
    </p>
    <p>
      A arquitetura da solução é composta por três camadas principais: o <strong>Frontend</strong>, a <strong>Automação com n8n</strong> e o <strong>Backend de IA</strong>.
    </p>
    
    <div class="architecture-details">
      <h3>Arquitetura da Aplicação</h3>
      <ul>
        <li>
          <strong>Frontend (Vue.js):</strong> O que você vê e interage. Uma página web simples com um formulário que coleta informações como idade, formação e experiência.
        </li>
        <li>
          <strong>Automação (n8n):</strong> Atua como um orquestrador. Quando você envia os dados no formulário, a requisição é recebida pelo <strong>n8n</strong>, que os processa e os encaminha para a API de IA.
        </li>
        <li>
          <strong>Backend de IA (Hugging Face):</strong> Uma API hospedada na plataforma Hugging Face que contém um modelo de inteligência artificial. Este modelo foi projetado e treinado a partir de um conjunto de dados fornecido pelo nosso professor. Sua função é receber os dados do seu perfil e predizer o cargo mais provável para você.
        </li>
      </ul>
    </div>
    
    <p>
      O resultado da predição é enviado de volta através do <strong>n8n</strong> para o <strong>Frontend</strong>, que exibe o cargo sugerido em uma nova modal, completando o fluxo do projeto.
    </p>
  </div>
</template>

<script setup>
</script>

<style scoped>
.about-card {
  max-width: 800px;
  padding: 2.5rem;
  text-align: left;
}

.about-card h2 {
  margin-bottom: 1.5rem;
}

.about-card p {
  font-size: 1rem;
  line-height: 1.6;
  color: var(--color-primary);
  margin-bottom: 1rem;
}

.architecture-details {
  background-color: var(--background-muted);
  border: 1px solid var(--border-secondary);
  border-radius: var(--border-radius-small);
  padding: 1.5rem;
  margin: 1.5rem 0;
}

.architecture-details h3 {
  margin-top: 0;
  color: var(--color-link);
  font-size: 1.25rem;
}

.architecture-details ul {
  list-style-type: none;
  padding-left: 0;
}

.architecture-details li {
  margin-bottom: 1rem;
  border-left: 2px solid var(--color-link);
  padding-left: 1rem;
}
</style>