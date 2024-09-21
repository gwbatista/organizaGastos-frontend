<!-- App.vue -->
<template>
  <v-app>
    <!-- Barra superior -->
    <v-app-bar app color="#37474F" dark>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>OrganizaGastos</v-toolbar-title>
    </v-app-bar>

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
export default {
  data() {
    return {
      drawer: true, // Controle do menu lateral
      menuItems: [
        { title: '2024', icon: 'mdi mdi-calendar-edit-outline', route: '/' },
        { title: 'Metas', icon: 'mdi mdi-bullseye-arrow', route: '/metas' }
      ],
    };
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