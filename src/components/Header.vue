<template>
  <header class="header-section">
    <div class="header-top">
      <div class="container">
        <div class="ht-left">
          <div class="mail-service">
            <i class=" fa fa-envelope"></i> hello.shayna@gmail.com
          </div>
          <div class="phone-service">
            <i class=" fa fa-phone"></i> +628 22081996
          </div>
        </div>
      </div>
    </div>
    <div class="container">
      <div class="inner-header">
        <div class="row">
          <div class="col-lg-2 col-md-2">
            <div class="logo">
              <router-link to="/">
                <img src="img/logo_website_shayna.png" alt="" />
              </router-link>
            </div>
          </div>
          <div class="col-lg-7 col-md-7"></div>
          <div class="col-lg-3 text-right col-md-3">
            <ul class="nav-right">
              <li class="cart-icon">
                Keranjang Belanja &nbsp;
                <a href="#">
                  <i class="icon_bag_alt"></i>
                  <span>{{keranjangUser.length}}</span>
                </a>
                <div class="cart-hover">
                  <div class="select-items">
                    <table>
                      <tbody>
                        
                        
                        <tr v-for="keranjang in keranjangUser" :key="keranjang.id">
                          <td class="si-pic">
                            <img class="photo-item" :src="keranjang.photo" alt="" />
                          </td>
                          <td class="si-text">
                            <div class="product-selected">
                              <p>${{keranjang.price}} x 1</p>
                              <h6>{{keranjang.name}}</h6>
                            </div>
                          </td>
                          <td class="si-close">
                            <i class="ti-close" @click="removeItem(keranjang.id)"></i>
                          </td>
                        </tr>


                      </tbody>
                    </table>
                  </div>
                  <div v-if="keranjangUser.length > 0">
                    <div class="select-total">
                      <span>total:</span>
                      <h5>${{totalHarga}}.00</h5>
                    </div>
                    <div class="select-button">
                      <a href="#" class="primary-btn view-card">VIEW CARD</a>
                      <router-link to="/cart" class="primary-btn checkout-btn">CHECK OUT</router-link>
                    </div>
                  </div>

                  <div v-else>
                    <h5 class="text-center">Tidak ada barang di keranjang</h5>
                  </div>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return{
        keranjangUser: []
    }
  },
  mounted(){
    if (localStorage.getItem('keranjangUser')) {
        try {
            this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
        } catch(e) {
            localStorage.removeItem('keranjangUser');
        }
      }
  },
  methods:{
    removeItem(idx){
      let keranjangUserStorage = JSON.parse(localStorage.getItem("keranjangUser"));
      let itemKeranjangUserStorage = keranjangUserStorage.map(itemKeranjangUserStorage => itemKeranjangUserStorage.id);

      let index = itemKeranjangUserStorage.findIndex(id => id == idx);
      this.keranjangUser.splice(index,1);

      const parsed = JSON.stringify(this.keranjangUser);
      localStorage.setItem('keranjangUser', parsed);
      window.location.reload();
    }
  },
  computed:{
    totalHarga(){
      return this.keranjangUser.reduce(function(items,data){
        return items + data.price;
      }, 0);
    }
  }
}
</script>

<style scoped>
.photo-item{
  height: 100px;
}
</style>
