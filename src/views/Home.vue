<template>
  <div>
    <GastoForm @gasto-adicionado="carregarGastos" />
    <GastoList ref="gastoList" />
  </div>
</template>

<script>
import GastoForm from '@/components/GastoForm.vue';
import GastoList from '@/components/GastoList.vue';

export default {
  components: {
    GastoForm,
    GastoList
  },
  methods: {
    carregarGastos() {
      this.$refs.gastoList.carregarGastos();
    }
  }
};
</script>
