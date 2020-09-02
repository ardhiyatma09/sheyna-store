<template>
  <div class="home">
    <Header/>
    <CarouselHero />
    <WomenBanner/>
    <Instagram/>
    <Partner/>
    <Footer/>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from "@/components/Header.vue";
import CarouselHero from "@/components/CarouselHero.vue";
import WomenBanner from "@/components/WomenBanner.vue";
import Instagram from "@/components/Instagram.vue";
import Partner from "@/components/Partner.vue";
import Footer from "@/components/Footer.vue";

export default {
  name: "Home",
  components: {
    Header,
    CarouselHero,
    WomenBanner,
    Instagram,
    Partner,
    Footer
  },
};
</script>
