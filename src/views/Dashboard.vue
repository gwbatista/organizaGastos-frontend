<template>
  <div>
    <h1>Dashboard</h1>
    <div class="charts-container">
      <GastosChart />
      <PessoalChart /> <!-- Adicione o segundo gráfico aqui -->
      <EmpresaChart /> <!-- Adicione o terceiro gráfico aqui -->
      <TotalChart /> <!-- Adicione o quarto gráfico aqui -->
    </div>
  </div>
</template>

<script>
import GastosChart from '@/components/GastosChart.vue';
import PessoalChart from '@/components/PessoalChart.vue';
import EmpresaChart from '@/components/EmpresaChart.vue';
import TotalChart from '@/components/TotalChart.vue';

export default {
  name: 'Dashboard',
  components: {
    GastosChart,
    PessoalChart,
    EmpresaChart,
    TotalChart
  }
};
</script>

<style scoped>
.charts-container {
  display: flex;
  flex-wrap: wrap; /* Permite que os gráficos se ajustem na linha seguinte */
  justify-content: space-between; /* Espaçamento igual entre os gráficos */
}

.charts-container > * {
  flex: 0 1 calc(50% - 10px); /* Cada gráfico ocupará 50% da largura menos uma margem */
  margin-bottom: 60px; /* Espaçamento vertical entre as linhas de gráficos */
}

@media (max-width: 768px) {
  .charts-container > * {
    flex: 0 1 100%; /* Em telas menores, os gráficos ocuparão toda a largura */
  }
}

h1 {
  font-weight: bold;
    font-size: 25px;
    margin-bottom: 14px
}
</style>
