<template>
  <div class="product">
    <MainHeader />

    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="breadcrumb-text product-more">
              <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
              <span>Detail</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="row">
              <div class="col-lg-6">
                <div class="product-pic-zoom">
                  <!-- <p :src="id"></p> -->
                  <img class="product-big-img" :src="image_default" alt="" />
                </div>
                <div
                  class="product-thumbs"
                  v-if="productDetails.galleries.length > 0"
                >
                  <carousel
                    class="product-thumbs-track ps-slider"
                    :dots="false"
                    :nav="false"
                  >
                    <div
                      v-for="ss in productDetails.galleries"
                      :key="ss.id"
                      class="pt"
                      @click="changeImage(ss.photo)"
                      :class="ss.photo == image_default ? 'active' : ''"
                    >
                      <img :src="ss.photo" alt="" />
                    </div>
                  </carousel>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="product-details">
                  <div class="pd-title">
                    <span>{{ productDetails.type }}</span>
                    <h3>{{ productDetails.name }}</h3>
                  </div>
                  <div class="pd-desc">
                    <p v-html="productDetails.description"></p>
                    <h4>${{ productDetails.price }}</h4>
                  </div>
                  <div class="quantity">
                    <router-link to="/cart">
                     <a @click="saveCart(productDetails.id, productDetails.name, productDetails.price, productDetails.galleries[0].photo)" href="#" class="primary-btn pd-cart">Add To Cart</a> 
                    </router-link>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Product Shop Section End -->

    <RelatedProduct />
    <MainFooter />
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import MainHeader from "../components/MainHeader.vue";
import MainFooter from "../components/MainFooter.vue";
import carousel from "vue-owl-carousel";
import RelatedProduct from "../components/RelatedProduct.vue";
import axios from "axios";

export default {
  name: "Product",
  components: {
    MainHeader,
    MainFooter,
    carousel,
    RelatedProduct,
  },
  data() {
    return {
      image_default: "",
      productDetails: [],
      cartProduct: [],
    };
  },
  methods: {
    changeImage(imageUrl) {
      this.image_default = imageUrl;
    },
    setDataPicture(data) {
      this.productDetails = data;

      this.image_default = data.galleries[0].photo;
    },
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
      .get("http://127.0.0.1:8000/api/products", {
        params: {
          id: this.$route.params.id,
        },
      })
      .then((res) => this.setDataPicture(res.data.data))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
.product-thumbs .pt {
  margin-right: 10px;
}
</style>
