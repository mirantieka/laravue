<template>
  <div>
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
      <div class="container-fluid">
        <div class="row">
          <div class="col-lg-12 mt-5" v-if="products.length > 0">
            <carousel :items="3" :nav="false" :autoplay="true" :dots="false">
              <div class="product-item" v-for="itemProduct in products" v-bind:key="itemProduct.id">
                <div class="pi-pic">
                  <img v-bind:src="itemProduct.galleries[0].photo" alt="" />
                  <ul>
                    <li class="w-icon active">
                      <a @click="saveCart(itemProduct.id, itemProduct.name, itemProduct.price, itemProduct.galleries[0].photo)" href="#"><i class="icon_bag_alt"></i></a>
                    </li>
                    <li class="quick-view">
                      <router-link v-bind:to="'/product/'+itemProduct.id">+ Quick View</router-link>
                    </li>
                  </ul>
                </div>
                <div class="pi-text">
                  <div class="catagory-name">{{itemProduct.type}}</div>
                  <a href="#">
                    <h5>{{itemProduct.name}}</h5>
                  </a>
                  <div class="product-price">
                    ${{itemProduct.price}}
                    <span>$50.00</span>
                  </div>
                </div>
              </div>
            </carousel>
          </div>
          <div class="col-lg-12" v-else>
            <p class="text-center">Produk tidak tersedia.</p>
          </div>
        </div>
      </div>
    </section>
    <!-- Women Banner Section End -->
  </div>
</template>

<script>
import carousel from "vue-owl-carousel";
import axios from "axios";
export default {
  name: "ProductCarousel",
  components: {
    carousel,
  },
  data() {
    return {
      products: [],
      cartProduct: []
    };
  },
  methods: {
    saveCart(idProduct, nameProduct, priceProduct, photoProduct) {

      var productStored = {
        "id": idProduct,
        "name": nameProduct,
        "price": priceProduct,
        "photo": photoProduct,
      }

      this.cartProduct.push(productStored);
      const parsed = JSON.stringify(this.cartProduct);
      localStorage.setItem('cartProduct', parsed);

      window.location.reload();
    }
  },
  mounted() {
    if (localStorage.getItem('cartProduct')) {
      try {
        this.cartProduct = JSON.parse(localStorage.getItem('cartProduct'));
      } catch(e) {
        localStorage.removeItem('cartProduct');
      }
    }
    axios
      .get("http://127.0.0.1:8000/api/products")
      .then((res) => (this.products = res.data.data.data))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
.product-item {
  margin-right: 25px;
}
</style>