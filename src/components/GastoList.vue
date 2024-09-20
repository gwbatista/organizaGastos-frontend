<template>
  <div>
    <h2>Lista de Gastos</h2>
    <ul>
      <li v-for="gasto in gastos" :key="gasto.id">
        {{ gasto.descricao }} - {{ gasto.valor }} - {{ gasto.data_vencimento }}
        <button @click="deletarGasto(gasto.id)">Deletar</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      gastos: []
    };
  },
  async created() {
    await this.carregarGastos();
  },
  methods: {
    async carregarGastos() {
      try {
        const response = await fetch('http://localhost:3000/gastos');
        if (!response.ok) {
          throw new Error('Erro ao buscar gastos');
        }
        const data = await response.json();
        this.gastos = data;
      } catch (error) {
        console.error('Erro ao carregar gastos:', error);
      }
    },
    async deletarGasto(id) {
      try {
        const response = await fetch(`http://localhost:3000/gastos/${id}`, {
          method: 'DELETE'
        });
        if (!response.ok) {
          throw new Error('Erro ao deletar gasto');
        }
        this.gastos = this.gastos.filter(gasto => gasto.id !== id);
      } catch (error) {
        console.error('Erro ao deletar gasto:', error);
      }
    }
  }
};
</script>
