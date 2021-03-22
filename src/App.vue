<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <router-link to="/">
        <h1>Madlib Game</h1>
      </router-link>
      <v-spacer></v-spacer>
      <router-link to="/create">
        <v-btn>Create Madlib</v-btn>
      </router-link>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  components: {},

  data: () => ({
    //
  }),
};
</script>

<style scoped>
a {
  text-decoration: none;
}
.router-link-active {
  color: rgb(255, 200, 100);
}
</style>
