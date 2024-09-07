<template>
    <div class="filtros">
      <div class="titulo">Filtrar</div>
      <div class="opcoes-filtros">
        <button
          class="botao"
          :class="{ ativo: filtroSelecionado === 'todos' }"
          @click="$emit('filtro-selecionado', 'todos')"
        >
          Todos
        </button>
        <button
          class="botao"
          :class="{ ativo: filtroSelecionado === 'gostei' }"
          @click="$emit('filtro-selecionado', 'gostei')"
        >
          Gostei
        </button>
        <button
          class="botao"
          :class="{ ativo: filtroSelecionado === 'nao-gostei' }"
          @click="$emit('filtro-selecionado', 'nao-gostei')"
        >
          Não Gostei
        </button>
      </div>
    </div>
  </template>
  
  <script setup>
  defineProps({
    filtroSelecionado: {
      type: String,
      required: true
    }
  })
  </script>
  
  <style scoped>
  .filtros {
    .titulo {
      font-weight: bold;
    }
  
    .opcoes-filtros {
      display: flex;
      gap: 10px;
    }
  
    .botao.ativo {
      background-color: #1976d2;
      color: white;
    }
  }
  </style>
  