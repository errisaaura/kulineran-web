<template>
  <div class="hero">
    <!-- dekstop -->
    <div class="d-none d-md-block">
      <div class="row mt-4">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <!-- <h2><strong>Delicious Food Menu, </strong> <br> in Your Gadget</h2> -->
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Delicious Food Menu, </strong> <br />
                in Your Gadget
              </h2>
              <p>Ayo segera pilih dan pesan makanan favorit anda</p>
              <!-- <router-link to="/" class="btn btn-lg btn-success">Pesan</router-link> -->
              <router-link class="btn btn-lg btn-success" to="/foods">
                <b-icon-arrow-right></b-icon-arrow-right>Pesan
              </router-link>
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <img src="../assets/Image/Hero.png" width="100%" />
        </div>
      </div>
    </div>

    <!-- mobile -->
    <div class="d-sm-block d-md-none">
      <div class="row mt-4">
           <div class="col-md-6 mb-3">
          <img src="../assets/Image/Hero.png" width="100%" />
        </div>
        <div class="col-md-6">
          <div class="d-flex h-100">
            <!-- <h2><strong>Delicious Food Menu, </strong> <br> in Your Gadget</h2> -->
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Delicious Food Menu, </strong> <br />
                in Your Gadget
              </h2>
              <p>Ayo segera pilih dan pesan makanan favorit anda</p>
              <!-- <router-link to="/" class="btn btn-lg btn-success">Pesan</router-link> -->
              <button class="btn btn-lg btn-success">
                <b-icon-arrow-right></b-icon-arrow-right>Pesan
              </button>
            </div>
          </div>
        </div>
       
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeroHome",
};
</script>

<style>
</style>