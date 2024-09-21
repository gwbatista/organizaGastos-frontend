<!-- Home.vue -->
<template>
  <v-container>
    <GastoList ref="gastoList" />
  </v-container>
</template>

<script>
import GastoList from '@/components/GastoList.vue';
import GuiList from '@/components/GuiList.vue';
import EmpresaList from '@/components/EmpresaList.vue';

export default {
  components: {
    GastoList
  },
  methods: {
    carregarGastos() {
      this.$refs.gastoList.carregarGastos();
      this.$refs.guiList.carregarGastos();
      this.$refs.empresaList.carregarGastos();
    }
  }
};
</script>
