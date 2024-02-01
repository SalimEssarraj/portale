<template>
  <v-app>
    <v-app-bar elevation="2">
      <template v-slot:prepend>
        <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      </template>

      <v-app-bar-title>Lista</v-app-bar-title>
    </v-app-bar>
    <v-navigation-drawer v-model="drawer" temporary>
      <v-divider></v-divider>
      <v-list>
        <v-list-item link>
         <v-list-item-content>
            <v-list-item-icon>
              <v-icon size="large" color="black">mdi-account</v-icon>
            </v-list-item-icon>
            <v-list-item-title @click="goUtenti">Utenti</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <v-divider></v-divider>
    </v-navigation-drawer>
     

    
      <router-view/>
  </v-app>
</template>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
<script>

export default {
  data() {
    return {
      drawer: null,
    }
  },
  methods: {
      goUtenti(){
        this.$router.push({ name: 'utenti' });
      }
    },
}
</script>