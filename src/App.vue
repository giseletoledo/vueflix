<template>
  <div class="vueflix">
    <FiltroFilmes :filtroSelecionado="filtroSelecionado" @filtro-selecionado="filtroSelecionado = $event" />
    
    <div v-if="estaAdicionandoNovo">
      <FormularioFilme @salvar="salvarNovoFilme" @cancelar="sairDoModoAdicao" />
    </div>
    
    <div v-else>
      <button class="botao ativo" @click="estaAdicionandoNovo = true">
        Adicionar Filme
      </button>
    </div>

    <div class="filmes">
      <FilmeItem 
        v-for="(filme, index) in filmesFiltrados" 
        :key="index" 
        :filme="filme" 
        :filmeIndex="index"
        @definir-like="definirLike"
        @excluir-filme="excluirFilme"
      />
    </div>
    
    <p v-if="filmesFiltrados.length === 0" style="flex: 1; text-align: center; align-self: center;">
      Nenhum filme encontrado
    </p>
  </div>
</template>

<script setup>
import { computed, ref, onMounted, watch } from 'vue'
import FiltroFilmes from './components/FiltroFilmes.vue'
import FilmeItem from './components/FilmeItem.vue'
import FormularioFilme from './components/FormularioFilme.vue'

const filmes = ref([])
const estaAdicionandoNovo = ref(false)
const filtroSelecionado = ref('todos')

const filmesFiltrados = computed(() => {
  switch (filtroSelecionado.value) {
    case 'gostei':
      return filmes.value.filter((item) => item.like === true)
    case 'nao-gostei':
      return filmes.value.filter((item) => item.like === false)
    default:
      return filmes.value
  }
})

const sairDoModoAdicao = () => {
  estaAdicionandoNovo.value = false
}

const salvarNovoFilme = (novoFilme) => {
  filmes.value.push(novoFilme)
  sairDoModoAdicao()
}

const excluirFilme = (index) => {
  const text = `Confirma a exclusão do filme ${filmes.value[index].nome}`
  if (confirm(text) === true) {
    filmes.value.splice(index, 1)
  }
}

const definirLike = (index, liked) => {
  filmes.value[index].like = liked
}

watch(
  () => filmes,
  (novo, velho) => {
    if (velho !== undefined) {
      localStorage.setItem('vueflix', JSON.stringify(filmes.value))
    }
  },
  { deep: true }
)

onMounted(() => {
  const dadosLocalStorage = localStorage.getItem('vueflix')
  if (dadosLocalStorage) {
    filmes.value = JSON.parse(dadosLocalStorage)
  }
})
</script>

<style scoped>
.vueflix {
  display: flex;
  flex-direction: column;
  padding: 16px;
  gap: 24px;
}

.filmes {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: space-evenly;
}
</style>
