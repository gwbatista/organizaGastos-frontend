<template>
  <div>
    <h2>Adicionar Gasto</h2>
    <form @submit.prevent="adicionarGasto">
      <div>
        <label for="descricao">Descrição:</label>
        <input type="text" v-model="descricao" required />
      </div>
      <div>
        <label for="valor">Valor:</label>
        <input type="number" v-model="valor" required />
      </div>
      <div>
        <label for="data_vencimento">Data de Vencimento:</label>
        <input type="date" v-model="data_vencimento" required />
      </div>
      <button type="submit">Adicionar</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      descricao: '',
      valor: '',
      data_vencimento: ''
    };
  },
  methods: {
    async adicionarGasto() {
      const response = await fetch('http://localhost:3000/gastos', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          descricao: this.descricao,
          valor: this.valor,
          data_vencimento: this.data_vencimento
        })
      });
      if (response.ok) {
        this.$emit('gasto-adicionado');
        this.descricao = '';
        this.valor = '';
        this.data_vencimento = '';
      } else {
        console.error('Erro ao adicionar gasto');
      }
    }
  }
};
</script>
