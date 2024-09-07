<template>
    <div class="adicionar-filme">
      <input type="text" autocomplete="off" placeholder="Nome do Filme" v-model="novoNome" />
      <input type="text" autocomplete="off" placeholder="URL da Imagem" v-model="novaImagemURL" />
      <input type="text" autocomplete="off" placeholder="Data de Lançamento" v-model="novoLancamento" />
      <input type="text" autocomplete="off" placeholder="Gênero" v-model="novoGenero" />
      <div class="acoes">
        <button class="botao ativo" @click="salvar">Salvar</button>
        <button class="botao danger ativo" @click="$emit('cancelar')">Cancelar</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'

const emit = defineEmits(['salvar', 'cancelar'])

  const novoNome = ref('')
  const novaImagemURL = ref('')
  const novoLancamento = ref('')
  const novoGenero = ref('')

const salvar = () => {
  try {
    console.log('Salvando filme...', novoNome.value)
    if (novoNome.value && novaImagemURL.value && novoLancamento.value && novoGenero.value) {
      emit('salvar', {
        nome: novoNome.value,
        imagem: novaImagemURL.value,
        lancamento: novoLancamento.value,
        genero: novoGenero.value,
        like: undefined
      })
} else {
      throw new Error('Todos os campos são obrigatórios')
    }
  } catch (error) {
    console.error('Erro ao salvar o filme:', error)
  }
}

const cancelar = () => {
  try {
    emit('cancelar')
  } catch (error) {
    console.error('Erro ao cancelar a operação:', error)
  }
}

  </script>
  
  <style scoped>
  .adicionar-filme {
    display: flex;
    gap: 10px;
  }
  </style>
  