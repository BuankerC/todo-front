<template>
  <div id="app">
    <div id="nav">
      <div v-if="isAuthenticated">
        <router-link to="/">Home</router-link>|
        <a href="#" @click.prevent="logout">logout</a>
      </div>
      <div v-else>
        <router-link to="/login">login</router-link>
      </div>
    </div>
    <div class="container">
      <router-view />
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data: function() {
    return {
      // isAuthenticated: this.$session.has("jwt")
      isAuthenticated: this.$store.getters.isAuthenticated
    };
  },
  methods: {
    logout: function() {
      // this.$session.destroy();
      this.$store.dispatch("logout");
      this.$router.push("/login");
    }
  },
  updated: function() {
    this.isAuthenticated = this.$store.getters.isAuthenticated;
  }
};
</script>
<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
