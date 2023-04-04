<template>
  <div>
    <p>Busca em Largura</p>
    <div>
      <label for="start">Início:</label>
      <input v-model="start" type="number" />
    </div>
    <div>
      <label for="target">Alvo:</label>
      <input v-model="target" type="number" />
    </div>
    <button class="search-button" @click="onSearch">Buscar</button>
    <div v-if="steps.length > 0" class="steps">
      Caminho: {{ steps.join(" -> ") }}
    </div>
    <div v-if="steps.length === 0 && searchClicked" class="not-found-message">
      Caminho não encontrado. Verifique os valores de início e alvo. =(
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      graph: {
        0: [1, 2],
        1: [0, 3, 4],
        2: [0, 5, 6],
        3: [1, 7, 8],
        4: [1, 9, 10],
        5: [2, 11, 12],
        6: [2, 13, 14],
        7: [3, 15, 16],
        8: [3, 17, 18],
        9: [4, 19, 20],
        10: [4, 21, 22],
        11: [5, 23, 24],
        12: [5, 25, 26],
        13: [6, 27, 28],
        14: [6],
        15: [7],
        16: [7],
        17: [8],
        18: [8],
        19: [9],
        20: [9],
        21: [10],
        22: [10],
        23: [11],
        24: [11],
        25: [12],
        26: [12],
        27: [13],
        28: [13, 29, 30],
        29: [28],
        30: [28, 31, 32],
        31: [30],
        32: [30],
      },
      start: 0,
      target: 0,
      steps: [],
      searchClicked: false,
    };
  },
  methods: {
    bfs(start, target) {
    const visited = new Set();
    const queue = [[start]];
    while (queue.length > 0) {
      const steps = queue.shift();
      const vertex = steps[steps.length - 1];
      if (vertex === target) {
        this.steps = steps;
        return true;
      }
      if (!visited.has(vertex)) {
        visited.add(vertex);
        const neighbors = this.graph[vertex] || [];
        for (const neighbor of neighbors) {
          if (!visited.has(neighbor)) {
            const newsteps = [...steps, neighbor];
            queue.push(newsteps);
          }
        }
      }
    }
    this.steps = [];
    return false;
  },
    onSearch() {
      this.searchClicked = true;
      this.steps = [];
      this.bfs(parseInt(this.start), parseInt(this.target));
    },
  },
};
</script>

<style>
.search-button {
  font-size: 1.2rem;
  padding: 10px;
  background-color: green;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.not-found-message {
  color: red;
  font-size: 2rem;
  font-weight: bold;
  margin-top: 20px;
}
label {
  display: block;
  margin-bottom: 10px;
  font-weight: bold;
}
input {
  padding: 10px;
  border: 2px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  margin-bottom: 20px;
}
.steps {
  margin-top: 20px;
  font-size: 2rem;
  font-weight: bold;
  color: green;
}
</style>
