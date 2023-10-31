<template>
  <div class="min-h-screen bg-gray-800 text-white selection:bg-indigo-500 selection:text-white">
    <NavigationMenu />
    <HomePage />
    <app-footer />

  </div>
</template>

<script>
import NavigationMenu from "./components/Navigation.vue";
import AppFooter from "./components/Footer.vue";
import HomePage from "./views/HomePage.vue";

export default {

  name: 'App',

  components: {
    NavigationMenu,
    HomePage,
    AppFooter
  },

}
</script>
