<!-- Home.vue -->
<template>
  <v-container>
    <GastoList ref="gastoList" />
  </v-container>
</template>

<script>
import GastoList from '@/components/GastoList.vue';

export default {
  components: {
    GastoList
  },
  methods: {
    carregarGastos() {
      this.$refs.gastoList.carregarGastos();
    }
  }
};
</script>
