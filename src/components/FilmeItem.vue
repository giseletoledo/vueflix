<template>
    <div class="filme">
      <div class="capa-container">
        <div class="acoes-filme">
          <button
            class="botao"
            :class="{ ativo: filme.like === true }"
            @click="$emit('definir-like', filmeIndex, true)"
          >
            Gostei
          </button>
          <button
            class="botao danger"
            :class="{ ativo: filme.like === false }"
            @click="$emit('definir-like', filmeIndex, false)"
          >
            Não Gostei
          </button>
          <button class="botao danger" @click="$emit('excluir-filme', filmeIndex)">Excluir</button>
        </div>
        <img class="capa" :src="filme.imagem" :alt="filme.nome" />
      </div>
      <div class="nome">{{ filme.nome }}</div>
      <div class="info">{{ filme.lancamento }} - {{ filme.genero }}</div>
    </div>
  </template>
  
  <script setup>
  defineProps({
    filme: {
      type: Object,
      required: true
    },
    filmeIndex: {
      type: Number,
      required: true
    }
  })
  </script>
  
  <style scoped>
  .filme {
    width: 200px;
    .capa-container {
      width: 100%;
      height: auto;
      position: relative;
      .capa {
        width: 100%;
        height: 100%;
      }
  
      .acoes-filme {
        position: absolute;
        bottom: 0;
        padding-bottom: 12px;
        background-image: linear-gradient(to bottom, rgba(255, 0, 0, 0), rgb(0, 0, 0));
        display: none;
        flex-direction: column;
        width: 100%;
        height: 100%;
        justify-content: flex-end;
      }
    }
  
    .nome {
      font-weight: bold;
    }
  
    .info {
      font-size: 12px;
    }
  
    &:hover {
      .acoes-filme {
        display: flex;
      }
    }
  }
  </style>
  