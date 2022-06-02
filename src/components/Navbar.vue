<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <div class="container">
          <b-navbar-brand href="#">Kulineran</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
            <router-link class="nav-link" to="/" >Home</router-link>
            <router-link class="nav-link" to="/foods">Foods</router-link>
         
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
            <router-link class="nav-link" to="/keranjang">Keranjang
                <b-icon-bag></b-icon-bag>
                <span class="badge badge-success ml-2">0</span>
            </router-link>

        </b-navbar-nav>
      </b-collapse>

      </div>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "NavbarMenu",
};
</script>

<style>
</style>