<template>
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
        <div class="container-fluid">
            <div class="row">
                <div class="col-lg-12 mt-5" v-if="products.length > 0">
                    <carousel class="product-slider" :nav="false" :autoplay="true" :dots="false">

                        <div class="product-item" v-for="product in products" :key="product.id">
                            <div class="pi-pic">
                                <img v-if="product.galleries[0]" :src="product.galleries[0].photo" alt="" />
                                <img src="https://via.placeholder.com/500x500.png" alt="" v-else>
                                <ul>
                                    <li class="w-icon active">
                                        <a href="#"><i class="icon_bag_alt"></i></a>
                                    </li>
                                    <li class="quick-view"><router-link :to="'/product/'+product.id">+ Quick View</router-link></li>
                                </ul>
                            </div>
                            <div class="pi-text">
                                <div class="catagory-name">{{product.type}}</div>
                                <router-link :to="'/product/'+product.id">
                                    <h5>{{product.name}}</h5>
                                </router-link>
                                <div class="product-price">
                                    ${{product.price}}
                                    <!-- <span>$35.00</span> -->
                                </div>
                            </div>
                        </div>

                    </carousel>
                </div>

                <div class="col-lg-12" v-else>
                    <p>data tidak di temukan</p>
                </div>
            </div>
        </div>
    </section>
    <!-- Women Banner Section End -->
</template>

<script>
import carousel from 'vue-owl-carousel'
import axios from 'axios'

export default {
    name: 'WomenBanner',
    components: {
        carousel,
  },
  data() {
      return{
          products: []
      }
  },
  mounted() {
      axios
        .get("http://127.0.0.1:8000/api/products")
        .then(res => (this.products = res.data.data.data))
        .catch(err => console.log(err));
  }
}
</script>

<style scoped>
.product-item{
    margin-right: 25px;
}
</style>