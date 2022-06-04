<template>
  <div class="keranjang">
    <Navbar :updateKeranjang="keranjangs" />
    <!-- <h2>Keranjang</h2> -->
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="text-dark">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Keranjang
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <h2>Keranjang <strong>Saya</strong></h2>
          <div class="table-responsive mt-5">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Foto</th>
                  <th scope="col">Makanan</th>
                  <th scope="col">Keterangan</th>
                  <th scope="col">Jumlah</th>
                  <th scope="col">Harga</th>
                  <th scope="col">Total Harga</th>
                  <th scope="col">Hapus</th>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="(keranjang, index) in keranjangs"
                  :key="keranjang.id"
                >
                  <th>{{ index + 1 }}</th>
                  <td>
                    <img
                      :src="'../assets/Image/' + keranjang.products.gambar"
                      class="img-fluid shadow"
                      width="250"
                    />
                  </td>
                  <td>
                    <strong>{{ keranjang.products.nama }}</strong>
                  </td>
                  <td>
                    {{ keranjang.keterangan ? keranjang.keterangan : "-" }}
                  </td>
                  <td>
                    {{ keranjang.jumlah_pemesanan }}
                  </td>
                  <td align="right">Rp. {{ keranjang.products.harga }}</td>
                  <td align="right">
                    <strong
                      >Rp.
                      {{
                        keranjang.products.harga * keranjang.jumlah_pemesanan
                      }}</strong
                    >
                  </td>
                  <td align="center" class="text-danger">
                    <b-icon-trash
                      @click="hapusKeranjang(keranjang.id)"
                    ></b-icon-trash>
                  </td>
                </tr>

                <!-- ini untuk penjumahan harga -->
                <tr>
                  <td colspan="6" align="right">
                    <strong>Total Harga : </strong>
                  </td>
                  <td align="right">
                    <strong>Rp. {{ totalHarga }}</strong>
                  </td>
                  <td></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>

      <!-- form checkout -->
      <div class="row justify-content-end">
        <div class="col-md-4">
          <form class="mt-4" v-on:checkout.prevent>
            <div class="form-group">
              <label for="nama">Nama : </label>
              <input type="text" class="form-control" v-model="pesan.nama" />
            </div>
            <div class="form-group">
              <label for="noMeja">Nomor Meja : </label>
              <input type="text" class="form-control" v-model="pesan.noMeja" />
            </div>

            <button
              type="checkout"
              class="btn btn-success float-right"
              @click="checkout"
            >
              <b-icon-cart></b-icon-cart> Checkout
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "KeranjangIni",
  components: {
    Navbar,
  },
  data() {
    return {
      keranjangs: [],
      pesan: {},
    };
  },
  methods: {
    setKeranjangs(data) {
      this.keranjangs = data;
    },

    hapusKeranjang(id) {
      axios
        .delete("http://localhost:3000/keranjangs/" + id)
        .then(() => {
          // console.log("Hapus : ", response)
          alert("Berhasil Hapus Product di keranjang");

          //update data keranjang
          axios
            .get("http://localhost:3000/keranjangs")
            .then((response) => this.setKeranjangs(response.data))
            .catch((error) => console.log(error));
        })
        .catch((error) => console.log(error));
    },

    checkout() {
      // eslint-disable-next-line no-empty
      if (this.pesan.nama && this.pesan.noMeja) {
        this.$router.push({path : "/pesanan-sukses"})
        this.pesan.keranjangs = this.keranjangs; //ini masukkan keranjang ke dalam pesan ini

        axios
          .post("http://localhost:3000/pesanans", this.pesan)
          .then(() => {
            alert("Sukses Dipesan");

            //ini untuk menghapus kernjang yang di navbar itu 
            //pakai map biar ga satu satu, soalnya di json cuman bisa satu satu
            this.keranjangs.map(function(item) {
                return axios
                    .delete("http://localhost:3000/keranjangs/" + item.id)
                    .catch((error) => console.log(error))

            })
            // this.$router.push({path : "/pesanan-sukses"})
            
          })
          .catch((error) => console.log(error));

      } else {
        alert("Nama dan Nomor Meja Harus Terisi");
      }
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => this.setKeranjangs(response.data))
      .catch((error) => console.log(error));
  },
  //   ini untuk penjumlahan total harga
  computed: {
    totalHarga() {
      return this.keranjangs.reduce(function (items, data) {
        return items + data.products.harga * data.jumlah_pemesanan;
      }, 0);
    },
  },
};
</script>

<style>
</style>