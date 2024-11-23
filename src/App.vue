<template>
  <v-app>
    <v-app-bar title="状态图生成器"></v-app-bar>
    <v-navigation-drawer>
      <v-list-item link title="生成器" href="#/"></v-list-item>
      <v-list-item link title="状态图Diagram配置" href="#/diagram"></v-list-item>
      <v-list-item link title="状态Status配置" href="#/status"></v-list-item>
      <v-list-item link title="位置Location配置" href="#/location"></v-list-item>
      <v-list-item link title="位置值StatusValue配置" href="#/value"></v-list-item>
    </v-navigation-drawer>

    <v-main class="d-flex align-center justify-center" style="min-height: 300px;">
      <component :is="currentView" />
    </v-main>
  </v-app>

</template>
<script lang="ts">

import DiagramConfig from './components/DiagramConfig.vue';
import LocationConfig from './components/LocationConfig.vue';
import StatusConfig from './components/StatusConfig.vue';
import StatusValueConfig from './components/StatusValueConfig.vue';
import Generator from './components/Generator.vue';

const routes = {
  '/': Generator,
  '/diagram': DiagramConfig,
  '/status': StatusConfig,
  '/location': LocationConfig,
  '/value': StatusValueConfig,
}

export default {
  data() {
    return {
      currentPath: window.location.hash
    }
  },
  computed: {
    currentView() {
      return routes[this.currentPath.slice(1) || '/'] || NotFound
    }
  },
  mounted() {
    window.addEventListener('hashchange', () => {
      this.currentPath = window.location.hash
    })
  }
}
</script>