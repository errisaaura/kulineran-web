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
                <span class="badge badge-success ml-2">{{updateKeranjang ? updateKeranjang.length : jumlah_pesanans.length  }}</span>
            </router-link>

        </b-navbar-nav>
      </b-collapse>

      </div>
    </b-navbar>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "NavbarMenu",
  data() {
    return {
      jumlah_pesanans : []
    }
  },
  //ini nanti digunakan untuk oper data jumlah item di kernajnag
  props : ['updateKeranjang'],
  methods : {
    setJumlah(data){
      this.jumlah_pesanans = data
    }
  },
  mounted(){
     axios
      .get("http://localhost:3000/keranjangs" )
      .then((response) => this.setJumlah(response.data))
      .catch((error) => console.log(error));
  }
};
</script>

<style>
</style>