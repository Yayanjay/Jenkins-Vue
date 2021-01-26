<template>
<div>
  <b-navbar toggleable="lg" type="light" variant="info">
    <b-navbar-brand href="#">NavBar</b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">

        <b-button variant="dark" class="mr-2">
          <router-link to="/login"> Login </router-link>
        </b-button>
        <b-button variant="dark" class="ml-2">Register</b-button>

      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</div>
</template>

<script>
// import Register from '../components/Regist';
// import Login from '../components/Login';
export default {
  name: "Home",
  data() {
    return {
      displayLogin: true
    }
  },
  components: {
    // Register,
    // Login
  },
  methods: {
    shuffleForm(value) {
      if (value === true) {
        this.displayLogin = false
      } else {
        this.displayLogin = true
      }
    }
  }

}
</script>

<style>
.vue-bg {
  background: #bce5d0;
}
</style>