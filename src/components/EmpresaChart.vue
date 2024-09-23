<template>
  <div>
    <canvas id="empresaChart"></canvas>
  </div>
</template>

<script>
import { Chart, registerables } from 'chart.js';

Chart.register(...registerables);

export default {
  name: 'EmpresaChart',
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
        const response = await fetch('http://localhost:3000/cempresa');
        if (!response.ok) {
          throw new Error('Erro ao buscar dados');
        }
        const data = await response.json();
        console.log(data);
        this.createChart(data);
      } catch (error) {
        console.error('Erro ao buscar dados', error);
      }
    },
    createChart(data) {
  const labels = data.map(item => item.descricao);

  // Meses a serem considerados
  const monthlyValues = [
    'janeiro', 'fevereiro', 'marco', 'abril', 'maio', 
    'junho', 'julho', 'agosto', 'setembro', 
    'outubro', 'novembro', 'dezembro'
  ];

  // Criação dos datasets para cada mês
  const datasets = monthlyValues.map((month) => {
    return {
      label: month.charAt(0).toUpperCase() + month.slice(1), // Capitaliza o nome do mês
      data: data.map(item => parseFloat(item[month]) || 0), // Converter para número
      backgroundColor: this.getRandomColor(),
      borderWidth: 1
    };
  });

  const ctx = document.getElementById('empresaChart').getContext('2d');
  this.chart = new Chart(ctx, {
    type: 'bar',
    data: {
      labels: labels,
      datasets: datasets
    },
    options: {
      responsive: true,
          plugins: {
            title: {
              display: true,
              text: 'Empresa', // Título do gráfico
              font: {
                size: 20 // Tamanho da fonte do título
              }
            }
          },
      scales: {
        y: {
          beginAtZero: true
        }
      }
    }
  });
},
getRandomColor() {
      const colorOptions = [
        'rgba(255, 165, 0, 0.6)', // Verde claro
        'rgba(255, 140, 0, 0.6)', // Azul
        'rgba(255, 99, 71, 0.6)',
        'rgba(178, 34, 34, 0.6)', // Cinza
      ];
      return colorOptions[Math.floor(Math.random() * colorOptions.length)];
    }
  }
};

</script>

<style scoped>
canvas {
  max-width: 100%; /* Para responsividade */
  height: 400px; /* Ajuste a altura conforme necessário */
  margin: auto;
}
</style>
