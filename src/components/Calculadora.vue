<template>
  <v-container>
    <v-card class="pa-4" max-width="400">
      <v-card-title>Calculadora</v-card-title>
      <v-card-text>
        <v-text-field v-model="input1" label="Número 1" type="number" outlined></v-text-field>
        <v-text-field v-model="input2" label="Número 2" type="number" outlined></v-text-field>
        <v-divider class="my-3"></v-divider>
        <div class="d-flex justify-space-between">
          <v-btn @click="calculate('+')">+</v-btn>
          <v-btn @click="calculate('-')">-</v-btn>
          <v-btn @click="calculate('*')">x</v-btn>
          <v-btn @click="calculate('/')">/</v-btn>
        </div>
      </v-card-text>
      <v-card-actions>
        <v-alert v-if="result !== null" type="info" class="mt-3">
          Resultado: {{ result }}
        </v-alert>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      input1: 0,
      input2: 0,
      result: null,
    };
  },
  methods: {
    calculate(operation) {
      const num1 = parseFloat(this.input1);
      const num2 = parseFloat(this.input2);

      switch (operation) {
        case '+':
          this.result = num1 + num2;
          break;
        case '-':
          this.result = num1 - num2;
          break;
        case '*':
          this.result = num1 * num2;
          break;
        case '/':
          this.result = num1 !== 0 && num2 !== 0 ? num1 / num2 : 'Divisão por zero!';
          break;
      }
    },
  },
};
</script>

<style scoped>
.v-btn {
  min-width: 56px;
}
</style>
