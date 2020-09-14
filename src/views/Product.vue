<template>
  <div class="product">
    <Header/>
    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="breadcrumb-text product-more text-left">
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
                                <img class="product-big-img" :src="gambar_default" alt="" />
                            </div>
                            <div class="product-thumbs" v-if="productDetails.galleries.length > 0">
                                <carousel class="product-thumbs-track ps-slider" :nav="false" :margin="10">
                                    <div class="pt" v-for="photo in productDetails.galleries" :key="photo.id" @click="changeImage(photo.photo)" :class="photo.photo == gambar_default ? 'active' : '' ">
                                        <img :src="photo.photo" alt="" />
                                    </div>
                                </carousel>
                            </div>
                        </div>
                        <div class="col-lg-6">
                            <div class="product-details text-left">
                                <div class="pd-title">
                                    <span>{{productDetails.type}}</span>
                                    <h3>{{productDetails.name}}</h3>
                                </div>
                                <div class="pd-desc">
                                    <p>
                                        {{productDetails.description}}
                                    </p>
                                    <h4>${{productDetails.price}}</h4>
                                </div>
                                <div class="quantity">
                                    <router-link to="/cart" class="primary-btn pd-cart">Add To Cart</router-link>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <!-- Product Shop Section End -->

    <RelatedProduct/>

    <Footer/>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";
import RelatedProduct from "@/components/RelatedProduct.vue";
import carousel from 'vue-owl-carousel'
import axios from 'axios'

export default {
  name: "product",
  components: {
    Header,
    Footer,
    carousel,
    RelatedProduct,
  },
  data() {
      return{
          idProduct: this.$route.params.id,
          productDetails:[],
          gambar_default: '',
          thumbs: [
              "img/mickey1.jpg",
              "img/mickey2.jpg",
              "img/mickey3.jpg",
              "img/mickey4.jpg"
          ],
      }
  },
  methods:{
      changeImage(urlImage) {
          this.gambar_default = urlImage;
          console.log(this.idProduct);
      },
      setDataPicture(data){
          this.productDetails = data;

          this.gambar_default = data.galleries[0].photo;
      }
  },
  mounted() {
      axios
        .get("http://127.0.0.1:8000/api/products",{
            params: {
                id: this.$route.params.id
            }
        })
        .then(res => (this.setDataPicture(res.data.data)))
        .catch(err => console.log(err));
  }
};
</script>