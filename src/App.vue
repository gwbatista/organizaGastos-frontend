<!-- App.vue -->
<template>
  <v-app>
    <!-- Barra superior -->
    <v-app-bar app color="#37474F" dark>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>OrganizaGastos</v-toolbar-title>
      <!-- Ícone da calculadora no lado direito -->
      <v-spacer></v-spacer> <!-- Espaçamento entre o título e o ícone -->
      <v-icon @click="dialog = true" class="mr-4" color="white">mdi-calculator</v-icon>
    </v-app-bar>

     <!-- Modal da Calculadora -->
    <v-dialog v-model="dialog" max-width="400">
      <Calculadora />
    </v-dialog>

    <!-- Menu lateral -->
<v-navigation-drawer v-model="drawer" app permanent width="100">
  <v-list dense>
    <v-list-item-group>
      <v-list-item
        v-for="(item, i) in menuItems"
        :key="i"
        @click="navigate(item.route)"
        class="mt-3 ml-4" 
      >
        <v-list-item-icon>
          <v-icon size="18">{{ item.icon }}</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title :style="{ fontSize: '15px' }">{{ item.title }}</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list-item-group>
  </v-list>
</v-navigation-drawer>

    <!-- Conteúdo principal -->
    <v-main>
      <v-container fluid>
        <router-view />
      </v-container>
    </v-main>

    <!-- Footer -->
    <v-footer app color="#37474F" dark class="d-flex justify-center align-center">
      <span class="footer">&copy; 2024 - Desenvolvido por Guilherme Watanabe</span>
    </v-footer>
  </v-app>
</template>

<script>
import Calculadora from './components/Calculadora.vue';

export default {
  data() {
    return {
      drawer: true, // Controle do menu lateral
      dialog: false, // Controle do modal da calculadora
      menuItems: [
        { title: '2024', icon: 'mdi mdi-calendar-edit-outline', route: '/' },
        { title: 'Metas', icon: 'mdi mdi-bullseye-arrow', route: '/metas' },
        { title: 'Dashboard', icon: 'mdi mdi-view-dashboard-outline', route: '/dashboard' }
      ],
    };
  },
  components: {
    Calculadora // Registrar o componente Calculator
  },
  methods: {
    navigate(route) {
      this.$router.push(route);
    }
  }
};
</script>

<style>
  .v-application {
    font-family: 'Roboto', sans-serif;
  }

  .footer {
    font-size: 12px; 
  }

</style>