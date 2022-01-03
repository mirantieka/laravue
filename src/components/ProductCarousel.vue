<template>
  <div>
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
      <div class="container-fluid">
        <div class="row">
          <div class="col-lg-12 mt-5">
            <carousel :items="3" :nav="false" :autoplay="true" :dots="false">
              <div class="product-item">
                <div class="pi-pic">
                  <img src="img/mickey1.jpg" alt="" />
                  <ul>
                    <li class="w-icon active">
                      <a href="#"><i class="icon_bag_alt"></i></a>
                    </li>
                    <li class="quick-view">
                      <router-link to="/product">+ Quick View</router-link>
                    </li>
                  </ul>
                </div>
                <div class="pi-text">
                  <div class="catagory-name">Bag</div>
                  <a href="#">
                    <h5>Mickey Baggy</h5>
                  </a>
                  <div class="product-price">
                    $14.00
                    <span>$35.00</span>
                  </div>
                </div>
              </div>
              <div class="product-item">
                <div class="pi-pic">
                  <img src="https://static.zara.net/photos///2021/I/0/1/p/6164/201/427/2/w/563/6164201427_6_1_1.jpg?ts=1629734104881" alt="" />
                  <ul>
                    <li class="w-icon active">
                      <a href="#"><i class="icon_bag_alt"></i></a>
                    </li>
                    <li class="quick-view"><a href="#">+ Quick View</a></li>
                  </ul>
                </div>
                <div class="pi-text">
                  <div class="catagory-name">Pants</div>
                  <a href="#">
                    <h5>Jeans Slim Fit</h5>
                  </a>
                  <div class="product-price">$34.00</div>
                </div>
              </div>
              <div class="product-item">
                <div class="pi-pic">
                  <img src="https://static.zara.net/photos///2021/I/1/1/p/1195/810/040/2/w/563/1195810040_6_1_1.jpg?ts=1633510171665" alt="" />
                  <ul>
                    <li class="w-icon active">
                      <a href="#"><i class="icon_bag_alt"></i></a>
                    </li>
                    <li class="quick-view"><a href="#">+ Quick View</a></li>
                  </ul>
                </div>
                <div class="pi-text">
                  <div class="catagory-name">Shoes</div>
                  <a href="#">
                    <h5>Rubber Boots</h5>
                  </a>
                  <div class="product-price">$40.00</div>
                </div>
              </div>
              <div class="product-item">
                <div class="pi-pic">
                  <img src="https://static.zara.net/photos///2021/I/0/1/p/3046/319/600/2/w/563/3046319600_6_1_1.jpg?ts=1634645098933" alt="" />
                  <ul>
                    <li class="w-icon active">
                      <a href="#"><i class="icon_bag_alt"></i></a>
                    </li>
                    <li class="quick-view"><a href="#">+ Quick View</a></li>
                    <li class="w-icon">
                      <a href="#"><i class="fa fa-random"></i></a>
                    </li>
                  </ul>
                </div>
                <div class="pi-text">
                  <div class="catagory-name">Jackets</div>
                  <a href="#">
                    <h5>Red Fleece Jacket</h5>
                  </a>
                  <div class="product-price">$37.50</div>
                </div>
              </div>
            </carousel>
          </div>
        </div>
      </div>
    </section>
    <!-- Women Banner Section End -->
  </div>
</template>

<script>
import carousel from 'vue-owl-carousel';
export default {
    name: 'ProductCarousel',
    components: {
        carousel
    }
}
</script>

<style>
.product-item {
    margin-right: 25px;
}
</style>