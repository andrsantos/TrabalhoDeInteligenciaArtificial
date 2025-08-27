<template>
  <div class="modal-overlay" @click.self="$emit('close')">
    <div class="card modal-card">
      <header class="modal-header">
        <h2 class="text-gradient">Complete seu perfil</h2>
        <button class="close-button" @click="$emit('close')">X</button>
      </header>
      
      <form v-if="!isLoading" @submit.prevent="submitForm">
        <div class="form-grid">
          
          <div class="form-field">
            <label for="dataNascimento" class="form-label">Data de nascimento</label>
            <input type="date" id="dataNascimento" v-model="formData.dataNascimento" class="form-input" required>
          </div>

          <div class="form-field">
            <label for="idade" class="form-label">Idade</label>
            <input type="number" id="idade" v-model="formData.idade" class="form-input buttonless" readonly style="border:none;">
            <!-- Elemento para exibir a mensagem de erro em tempo real -->
            <p v-if="idadeError" class="error-message">{{ idadeError }}</p>
          </div>

          <div class="form-field">
            <label for="tempoExperiencia" class="form-label">Tempo de experiência com dados</label>
            <select id="tempoExperiencia" v-model="formData.tempoExperiencia" class="form-select" required>
              <option disabled value="">Selecione a experiência</option>
              <option>Menos de 1 ano</option>
              <option>De 1 a 2 anos</option>
              <option>De 2 a 3 anos</option>
              <option>De 3 a 5 anos</option>
              <option>Mais de 5 anos</option>
            </select>
          </div>
          
          <div class="form-field">
            <label for="formacao" class="form-label">Formação</label>
            <select id="formacao" v-model="formData.formacao" class="form-select" required>
              <option disabled value="">Selecione uma opção</option>
              <option>Computação / Engenharia de Software / Sistemas de Informação/TI</option>
              <option>Outras Engenharias</option>
              <option>Estatística / Matemática / Matemática Computacional / Ciências Atuariais</option>
              <option>Ciências Biológicas / Farmácia / Medicina / Área da Saúde</option>
              <option>Ciências Sociais</option>
              <option>Economia / Administração / Contabilidade / Finanças / Negócios</option>
              <option>Marketing / Publicidade / Comunicação / Jornalismo</option>
              <option>Química / Física</option>
              <option>Outra opção</option>
            </select>
          </div>

          <div class="form-field">
            <label for="nivelEnsino" class="form-label">Nível de Ensino</label>
            <select id="nivelEnsino" v-model="formData.nivelEnsino" class="form-select" required>
              <option disabled value="">Selecione um nível</option>
              <option>Pós-graduação</option>
              <option>Graduação/Bacharelado</option>
              <option>Doutorado ou Phd</option>
              <option>Estudante de Graduação</option>
              <option>Mestrado</option>
              <option>Não tenho graduação formal</option>
              <option>Prefiro não informar</option>
            </select>
          </div>

          <div class="form-field radio-group">
            <label class="form-label">Vive no Brasil?</label>
            <div>
              <input type="radio" id="viveSim" value="Sim" v-model="formData.viveNoBrasil" required>
              <label for="viveSim">Sim</label>
            </div>
            <div>
              <input type="radio" id="viveNao" value="Não" v-model="formData.viveNoBrasil">
              <label for="viveNao">Não</label>
            </div>
          </div>
          
          <div class="form-field full-width" v-if="formData.viveNoBrasil === 'Sim'">
            <label for="estado" class="form-label">Estado de Moradia</label>
            <select id="estado" v-model="formData.estado" class="form-select" :required="formData.viveNoBrasil === 'Sim'">
              <option disabled value="">Selecione um estado</option>
              <option>Acre</option>
              <option>Alagoas</option>
              <option>Amapá</option>
              <option>Amazonas</option>
              <option>Bahia</option>
              <option>Ceará</option>
              <option>Distrito Federal</option>
              <option>Espírito Santo</option>
              <option>Goiás</option>
              <option>Maranhão</option>
              <option>Mato Grosso</option>
              <option>Mato Grosso do Sul</option>
              <option>Minas Gerais</option>
              <option>Pará</option>
              <option>Paraíba</option>
              <option>Paraná</option>
              <option>Pernambuco</option>
              <option>Piauí</option>
              <option>Rio de Janeiro</option>
              <option>Rio Grande do Norte</option>
              <option>Rio Grande do Sul</option>
              <option>Rondônia</option>
              <option>Roraima</option>
              <option>Santa Catarina</option>
              <option>São Paulo</option>
              <option>Sergipe</option>
              <option>Tocantins</option>
            </select>
          </div>
          
          <div class="form-field">
            <label class="form-label">Linguagem Preferida</label>
            <div class="checkbox-group" id="linguagem">
              <div class="checkbox-option" v-for="option in linguagemOptions" :key="option">
                <input type="checkbox" :id="'lang-' + option" :value="option" v-model="formData.linguagem">
                <label :for="'lang-' + option">{{ option }}</label>
              </div>
            </div>
          </div>

          <div class="form-field">
            <label for="cloud" class="form-label">Cloud Preferida</label>
            <select id="cloud" v-model="formData.cloud" class="form-select" required>
              <option disabled value="">Selecione uma cloud</option>
              <option>Amazon Web Services (AWS)</option>
              <option>Google Cloud (GCP)</option>
              <option>Azure (Microsoft)</option>
              <option>Não sei opinar</option>
              <option>Outra Cloud</option>
            </select>
          </div>

          <div class="form-field">
            <label class="form-label">Banco de Dados Preferido</label>
            <div class="checkbox-group" id="bancoDados">
              <template v-for="(options, group) in bancoDadosOptions" :key="group">
                <div class="optgroup-label">{{ group }}</div>
                <div class="checkbox-option" v-for="option in options" :key="option">
                  <input type="checkbox" :id="'db-' + option" :value="option" v-model="formData.bancoDados">
                  <label :for="'db-' + option">{{ option }}</label>
                </div>
              </template>
            </div>
          </div>
        </div>
        <div class="form-actions">
          <button type="submit" class="card-button-primary" :disabled="isLoading || idadeError">
            Enviar
          </button>
        </div>
      </form>

      <div v-else class="loading-state">
        <div class="spinner"></div>
        <p>Enviando dados...</p>
      </div>

    </div>
  </div>
</template>

<script setup>
import { ref, watch, defineEmits } from 'vue';

const emit = defineEmits(['close', 'prediction-ready']);

const formData = ref({
  dataNascimento: '',
  idade: null,
  tempoExperiencia: '',
  formacao: '',
  nivelEnsino: '',
  viveNoBrasil: '',
  estado: '',
  linguagem: [],
  cloud: '',
  bancoDados: []
});

const isLoading = ref(false);
const idadeError = ref(null); // Novo estado para a mensagem de erro da idade

const linguagemOptions = [
  'Nenhuma', 'A BAP', 'ABAP', 'C++', 'C', 'C#', 'Clipper', 'COBOL', 'Delphi', 'Elixir', 'F#', 'Go', 'HTML', 'Java', 'JavaScript', 'Kotlin', 'Lisp', 'M', 'Matlab', 'Pascal', 'Perl', 'PHP', 'Python', 'R', 'Ruby', 'Rust', 'Scala', 'Softwares estatísticos', 'SQL', 'Swift', 'TypeScript', 'Visual Basic', 'Outra'
];

const bancoDadosOptions = {
  'Plataformas de Nuvem': ['Microsoft Azure', 'Google Cloud', 'Amazon', 'SAP'],
  'Bancos de Dados Relacionais': ['SQL', 'MySQL', 'PostgreSQL', 'Oracle', 'SQLite', 'MariaDB', 'DB2', 'Sybase'],
  'Bancos de Dados NoSQL': ['MongoDB', 'DynamoDB', 'Neo4J', 'Cassandra', 'Firebase', 'HBase'],
  'Outras Ferramentas e Fontes': ['Nenhum/Outro', 'Excel', 'Fontes não estruturadas', 'Access', 'API', 'ClickHouse', 'Databricks', 'Hadoop', 'Hive', 'Metabase', 'Redis', 'Snowflake', 'Splunk', 'Teradata', 'Outro']
};

watch(() => formData.value.dataNascimento, (novaData) => {
  if (!novaData) {
    formData.value.idade = null;
    idadeError.value = null;
    return;
  }
  const hoje = new Date();
  const dataNasc = new Date(novaData);
  let idadeCalculada = hoje.getFullYear() - dataNasc.getFullYear();
  const mes = hoje.getMonth() - dataNasc.getMonth();
  if (mes < 0 || (mes === 0 && hoje.getDate() < dataNasc.getDate())) {
    idadeCalculada--;
  }
  formData.value.idade = idadeCalculada;
  
  // Verificação em tempo real
  if (idadeCalculada < 18) {
    idadeError.value = 'A idade deve ser 18 anos ou mais.';
  } else {
    idadeError.value = null;
  }
});

watch(() => formData.value.viveNoBrasil, (novoValor) => {
  if (novoValor === 'Não') {
    formData.value.estado = '';
  }
});

const submitForm = async () => {
  // Validação de idade no envio, agora com o estado reativo
  if (idadeError.value) {
    alert('Por favor, corrija a idade antes de continuar.');
    return;
  }
  
  const campos = Object.keys(formData.value);
  for (const campo of campos) {
    const valor = formData.value[campo];
    if (campo === 'estado' && formData.value.viveNoBrasil === 'Não') {
      continue;
    }
    if ((typeof valor === 'string' && !valor) || (Array.isArray(valor) && valor.length === 0)) {
      if (campo !== 'idade') {
        alert('Por favor, preencha todos os campos obrigatórios.');
        return;
      }
    }
  }

  isLoading.value = true;

  const requestPayload = {
    inputs: {
      idade: formData.value.idade,
      linguagens_preferidas: formData.value.linguagem.join(', '),
      bancos_de_dados: formData.value.bancoDados.join(', '),
      vive_no_brasil: formData.value.viveNoBrasil,
      estado_moradia: formData.value.estado,
      nivel_ensino: formData.value.nivelEnsino,
      formacao: formData.value.formacao,
      tempo_experiencia_dados: formData.value.tempoExperiencia
    },
    chatId: 0
  };

  console.log("Requisição", JSON.stringify(requestPayload));

  try {
    const response = await fetch('https://andreyrsantos.app.n8n.cloud/webhook/b083795b-3671-4ec5-92d3-0e4952638003', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(requestPayload)
    });
    const data = await response.json();
    emit('prediction-ready', data.predicted_cargo);
  } catch (error) {
    console.error('Erro ao enviar o formulário:', error);
    alert('Ocorreu um erro ao enviar os dados. Por favor, tente novamente.');
  } finally {
    isLoading.value = false;
  }
};
</script>

<style scoped>
/* Estilos da modal e form (não alterados) */
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

.modal-card {
  position: relative;
  padding: 2rem;
  min-width: 450px;
  max-width: 700px;
  max-height: 80vh;
  overflow-y: auto;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.close-button {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
}

.form-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

.form-field {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.full-width {
  grid-column: 1 / -1;
}

.form-label {
  font-weight: 600;
  color: var(--color-primary);
  font-size: 0.875rem;
}

.form-input,
.form-select {
  padding: 0.5rem 0.75rem;
  border: 1px solid var(--border-secondary);
  border-radius: var(--border-radius-small);
  background: var(--background-muted);
  color: var(--color-primary);
  width: 100%;
}

.radio-group {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.radio-group div {
  display: flex;
  align-items: center;
}

.radio-group input {
  margin-right: 8px;
}

.form-actions {
  margin-top: 20px;
  text-align: right;
}

/* Estilos dos checkboxes (não alterados) */
.checkbox-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  padding: 0.75rem;
  border: 1px solid var(--border-secondary);
  border-radius: var(--border-radius-small);
  background: var(--background-muted);
  max-height: 200px;
  overflow-y: auto;
}

.checkbox-option {
  display: flex;
  align-items: center;
  gap: 8px;
  color: var(--color-primary);
}

.checkbox-option input[type="checkbox"] {
  appearance: none;
  width: 16px;
  height: 16px;
  border: 1px solid var(--border-secondary);
  background-color: transparent;
  border-radius: 4px;
  cursor: pointer;
  position: relative;
  transition: all 0.2s;
}

.checkbox-option input[type="checkbox"]:checked {
  background-color: var(--color-link);
  border-color: var(--color-link);
}

.checkbox-option input[type="checkbox"]:checked::before {
  content: '✓';
  color: var(--background-primary);
  font-size: 10px;
  font-weight: bold;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.optgroup-label {
  font-weight: 700;
  color: var(--color-link);
  margin-top: 0.5rem;
  padding-bottom: 0.25rem;
  border-bottom: 1px dashed var(--border-secondary);
  margin-bottom: 0.5rem;
}

/* NOVOS ESTILOS PARA A ANIMAÇÃO DE CARREGAMENTO */
.loading-state {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  min-height: 250px;
  gap: 1rem;
}

.spinner {
  border: 4px solid rgba(255, 255, 255, 0.3);
  border-top: 4px solid var(--color-link);
  border-radius: 50%;
  width: 50px;
  height: 50px;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

/* NOVO ESTILO PARA A MENSAGEM DE ERRO */
.error-message {
  color: #ff6b6b; /* Cor vermelha para o erro */
  font-size: 0.8rem;
  margin-top: 5px;
}
</style>
