<template>
  <div id="app">
    <h1>Algoritmo de Busca em Largura e Profundidade</h1>
    <h2>Trabalho Final da primeira etapa da disciplina Teoria dos Grafos</h2>

    <div class="areaButtons">
      <button
        :class="{ active: searchType === 'dfs' }"
        @click="onDfsClick"
        class="button"
      >
        Busca em Profundidade
      </button>
      <button
        :class="{ active: searchType === 'bfs' }"
        @click="onBfsClick"
        class="button"
      >
        Busca em Largura
      </button>
    </div>

    <p v-if="searchType === ''">Escolha seu método de busca.</p>

    <DfsAlgorithm v-if="searchType === 'dfs'" />
    <BfsAlgorithm v-if="searchType === 'bfs'" />

    <h4>
      <a
        href="https://github.com/alofrrr/Busca-Profundidade-Largura" target="_blank">
        Visuarizar código no GitHub
      </a>
    </h4>
  </div>
</template>

<script>
import DfsAlgorithm from "./components/DfsAlgorithm.vue";
import BfsAlgorithm from "./components/BfsAlgorithm.vue";

export default {
  components: {
    DfsAlgorithm,
    BfsAlgorithm,
  },
  data() {
    return {
      searchType: "",
    };
  },
  methods: {
    onDfsClick() {
      this.searchType = "dfs";
    },
    onBfsClick() {
      this.searchType = "bfs";
    },
  },
};
</script>

<style>
body {
  font-family: "Lato", sans-serif;

  background: linear-gradient(
    90deg,
    rgba(2, 0, 36, 1) 0%,
    rgba(9, 9, 121, 1) 31%,
    rgba(0, 212, 255, 1) 100%
  );
  color: #fff;
}

#app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  height: 90vh;
}

#app h1 {
  margin-bottom: 10px;
  font-weight: 300;
  font-size: 3rem;
}

#app h2 {
  font-weight: 300;
  font-size: 1.5rem;
}
#app p {
  font-weight: 300;
  font-size: 1.5rem;
}
.active {
  background-color: darkmagenta;
  color: white;
}
.button {
  padding: 10px;
  border: none;
  border-radius: 5px;
  margin: 10px;
  font-size: 1.2rem;
  cursor: pointer;
}
a{
  color: white;
  text-decoration: none;
}
</style>
