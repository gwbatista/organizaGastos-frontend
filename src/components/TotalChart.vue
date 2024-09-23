<template>
  <div>
    <canvas id="totalChart"></canvas>
  </div>
</template>

<script>
import { Chart, registerables } from 'chart.js';

Chart.register(...registerables);

export default {
  name: 'TotalChart',
  data() {
    return {
      chart: null,
    };
  },
  mounted() {
    this.fetchGastos();
  },
  methods: {
    async fetchGastos() {
      try {
        const response = await fetch('http://localhost:3000/ctotal'); // Substitua pela sua rota
        if (!response.ok) {
          throw new Error('Erro ao buscar dados');
        }
        const data = await response.json();
        this.createChart(data);
      } catch (error) {
        console.error('Erro ao buscar dados', error);
      }
    },
    createChart(data) {
  const months = data.map(item => item.mes);
  const moradia = data.map(item => parseFloat(item.moradia)); // Converta para número
  const pessoal = data.map(item => parseFloat(item.pessoal)); // Converta para número
  const empresa = data.map(item => parseFloat(item.empresa)); // Converta para número

  const totalPorMes = moradia.map((value, index) => value + pessoal[index] + empresa[index]);
  
  const porcentagemMoradia = moradia.map((value, index) => 
    totalPorMes[index] !== 0 ? (value / totalPorMes[index]) * 100 : 0
  );
  
  const porcentagemPessoal = pessoal.map((value, index) => 
    totalPorMes[index] !== 0 ? (value / totalPorMes[index]) * 100 : 0
  );
  
  const porcentagemEmpresa = empresa.map((value, index) => 
    totalPorMes[index] !== 0 ? (value / totalPorMes[index]) * 100 : 0
  );

  // Dados para o gráfico
  const dataValues = [
    porcentagemMoradia.reduce((acc, val) => acc + val, 0) / months.length,
    porcentagemPessoal.reduce((acc, val) => acc + val, 0) / months.length,
    porcentagemEmpresa.reduce((acc, val) => acc + val, 0) / months.length,
  ];

  const ctx = document.getElementById('totalChart').getContext('2d');
  this.chart = new Chart(ctx, {
    type: 'pie',
    data: {
      labels: ['Moradia', 'Pessoal', 'Empresa'],
      datasets: [{
        label: 'Gastos (%)',
        data: dataValues,
        backgroundColor: [
         'rgba(54, 162, 235, 0.6)',
          'rgba(75, 192, 192, 0.6)',
          'rgba(255, 99, 132, 0.6)',
        ],
      }],
    },
    options: {
      responsive: true,
      plugins: {
        legend: {
          display: true,
          position: 'top',
        },
        title: {
          display: true,
          text: 'Distribuição de Gastos por Categoria (%)',
        },
      },
    },
  });
}
  }
};
</script>

<style scoped>
canvas {
  max-width: 100%;
  height: 400px; /* Ajuste a altura conforme necessário */
  margin: auto;
}
</style>
