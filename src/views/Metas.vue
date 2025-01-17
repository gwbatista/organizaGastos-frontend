<!-- Home.vue -->
<template>
  <v-container>
    <MetasList ref="metasList" />
  </v-container>
</template>

<script>
import MetasList from '@/components/MetasList.vue';

export default {
  components: {
    MetasList,
  },
  methods: {
    carregarGastos() {
      this.$refs.metasList.carregarGastos();
    }
  }
};
</script>
