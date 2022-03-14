<template>
  <div>
    <MainHeader />
    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="breadcrumb-text product-more">
              <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
              <span>Shopping Cart</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Shopping Cart Section Begin -->
    <section class="shopping-cart spad">
      <div class="container">
        <div class="row">
          <div class="col-lg-8">
            <div class="row">
              <div class="col-lg-12">
                <div class="cart-table">
                  <table>
                    <thead>
                      <tr>
                        <th>Image</th>
                        <th class="p-name text-center">Product Name</th>
                        <th>Price</th>
                        <th>Action</th>
                      </tr>
                    </thead>
                    <tbody>
                      <tr v-for="cart in cartProduct" :key="cart.id">
                        <td class="cart-pic first-row">
                          <img class="photo-item" v-bind:src="cart.photo" />
                        </td>
                        <td class="cart-title first-row text-center">
                          <h5>{{ cart.name }}</h5>
                        </td>
                        <td class="p-price first-row">${{ cart.price }}</td>
                        <td class="delete-item">
                          <a @click="removeItem(cartProduct.index)" href="#"
                            ><i class="material-icons"> close </i></a
                          >
                        </td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
              <div class="col-lg-8">
                <h4 class="mb-4">Informasi Pembeli:</h4>
                <div class="user-checkout">
                  <form>
                    <div class="form-group">
                      <label for="namaLengkap">Nama lengkap</label>
                      <input
                        type="text"
                        class="form-control"
                        id="namaLengkap"
                        aria-describedby="namaHelp"
                        placeholder="Masukan Nama"
                        v-model="customerInfo.name"
                      />
                    </div>
                    <div class="form-group">
                      <label for="namaLengkap">Email Address</label>
                      <input
                        type="email"
                        class="form-control"
                        id="emailAddress"
                        aria-describedby="emailHelp"
                        placeholder="Masukan Email"
                        v-model="customerInfo.email"
                      />
                    </div>
                    <div class="form-group">
                      <label for="namaLengkap">No. HP</label>
                      <input
                        type="text"
                        class="form-control"
                        id="noHP"
                        aria-describedby="noHPHelp"
                        placeholder="Masukan No. HP"
                        v-model="customerInfo.number"
                      />
                    </div>
                    <div class="form-group">
                      <label for="alamatLengkap">Alamat Lengkap</label>
                      <textarea
                        class="form-control"
                        id="alamatLengkap"
                        rows="3"
                        v-model="customerInfo.address"
                      ></textarea>
                    </div>
                  </form>
                </div>
              </div>
            </div>
          </div>
          <div class="col-lg-4">
            <div class="row">
              <div class="col-lg-12">
                <div class="proceed-checkout">
                  <ul>
                    <li class="subtotal">
                      ID Transaction <span>#SH12000</span>
                    </li>
                    <li class="subtotal mt-3">
                      Subtotal <span>${{ totalPrice }}.00</span>
                    </li>
                    <li class="subtotal mt-3">
                      Pajak <span>${{ totalTax }}0</span>
                    </li>
                    <li class="subtotal mt-3">
                      Total Biaya <span>${{ totalCost }}0</span>
                    </li>
                    <li class="subtotal mt-3">
                      Bank Transfer <span>Mandiri</span>
                    </li>
                    <li class="subtotal mt-3">
                      No. Rekening <span>2208 1996 1403</span>
                    </li>
                    <li class="subtotal mt-3">
                      Nama Penerima <span>Shayna</span>
                    </li>
                  </ul>
                  <!-- <router-link @click="checkout()" to="/success" class="proceed-btn"
                    >I ALREADY PAID</router-link
                  > -->
                  <a href="#" @click="checkout()" class="proceed-btn">I ALREADY PAID</a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Shopping Cart Section End -->
  </div>
</template>

<script>
import MainHeader from "../components/MainHeader.vue";
import axios from "axios";
export default {
  name: "ShoppingCart",
  components: {
    MainHeader,
  },
  data() {
    return {
      cartProduct: [],
      customerInfo: {
        name: "",
        email: "",
        number: "",
        address: "",
      },
    };
  },
  methods: {
    removeItem(index) {
      this.cartProduct.splice(index, 1);
      const parsed = JSON.stringify(this.cartProduct);
      localStorage.setItem("cartProduct", parsed);
    },
    //fungsi untuk mengirim data ke API
    checkout() {
      let productIds = this.cartProduct.map(function (product) {
        return product.id;
      });

      let checkoutData = {
        'name': this.customerInfo.name,
        'email': this.customerInfo.email,
        'number': this.customerInfo.number,
        'address': this.customerInfo.address,
        "transaction_total": this.totalCost,
        "transaction_status": "PENDING",
        "transaction_details": productIds
      };

      axios
        .post("http://127.0.0.1:8000/api/checkout", checkoutData)
        .then(() => this.$router.push('success'))
        .catch((err) => console.log(err));
    },
  },
  mounted() {
    if (localStorage.getItem("cartProduct")) {
      try {
        this.cartProduct = JSON.parse(localStorage.getItem("cartProduct"));
      } catch (e) {
        localStorage.removeItem("cartProduct");
      }
    }
  },
  computed: {
    totalPrice() {
      return this.cartProduct.reduce(function (items, data) {
        return items + data.price;
      }, 0);
    },
    totalTax() {
      return (this.totalPrice * 10) / 100;
    },
    totalCost() {
      return parseInt(this.totalPrice + this.totalTax);
    },
  },
};
</script>

<style scoped>
.photo-item {
  width: 100px;
  height: 120px;
}
</style>