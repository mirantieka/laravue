<template>
  <div class="home">
    <MainHeader />
    <MainCarousel />
    <ProductCarousel />
    <Insta />
    <Partner />
    <MainFooter />
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import MainHeader from '../components/MainHeader.vue';
import MainCarousel from '../components/MainCarousel.vue';
import ProductCarousel from '../components/ProductCarousel.vue';
import Insta from '../components/Insta.vue';
import Partner from '../components/Partner.vue';
import MainFooter from '../components/MainFooter.vue';

export default {
  name: "Home",
  components: {
    MainHeader,
    MainCarousel,
    ProductCarousel,
    Insta,
    Partner,
    MainFooter
  },
};
</script>
