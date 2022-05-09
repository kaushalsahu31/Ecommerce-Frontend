<template>
  <div class="custom-container">
    <Header />
    <div class="breadcrumbs">
      <div class="div">
        <router-link to="/" class="link">Home</router-link> > <div class="crumbs"> {{productdetails.name}}</div>
      </div>
      
    </div>
    <div class="product-main">
      <div class="crosal">
        <VueSlickCarousel :slidesToShow= 2
          :slidesToScroll= 1 :arrows="true" :infinity="true" :speed="2000" :autoplaySpeed="2000" :autoplay="true" :dots="true" >
          <div v-for="(val, i) in gallery" :key="i" class="crozalimg"><img :src="val.image" alt="" /></div>
          
        </VueSlickCarousel>
      </div>
      <div class="productdetail">
        <div class="topbox">
          <div class="heading">{{ productdetails.name }}</div>
          <div class="stars"></div>
          <div class="price">
            ₹{{ productdetails.selling_price }}
            <span v-if="productdetails.selling_price!==productdetails.price" class="discount">{{ productdetails.discount }}% off</span>
          </div>
          <div v-if="productdetails.selling_price!==productdetails.price" class="mrp">
            MRP:₹<strike>{{ productdetails.price }}</strike> (inclusive of all
            taxes)
          </div>
          <div v-else class="mrp">
            (inclusive of all taxes)
          </div>
        </div>
        <div class="second">
          VIP Club Member get an extra discount of Rs.60 and Free Shipping.
          <strong class="clickable">Learn More</strong>
        </div>
        <div class="third">
          <div class="color">Colour : {{ productdetails.color }}</div>
          <div class="variation">
            <div
              v-for="(val, i) in productdetails.variation"
              :key="i"
              class="variationImg"
            >
              <img :src="val.image" alt="" />
            </div>
          </div>
          <div class="size">
            <div class="label">SIZE : L</div>
            <strong><u>SIZE CHART</u></strong>
          </div>
          <div class="sizes">
            <div class="sizelist" v-for="(val, i) in size.split(',')" :key="i">
              {{ val.slice(1, val.length - 1) }}
            </div>
          </div>
          <div class="fitinfo">
            Fit info
            <div v-if="productdetails.fit!==''" class="likebtns">{{ productdetails.fit }}</div>
          </div>
          <div class="modals">
            Modal
            <div class="likebtns">{{ productdetails.fit }}</div>
            <div class="likebtns">{{ productdetails.fit }}</div>
          </div>
          <div class="tobag">
            <div class="addtobag"><button class="bag">ADD TO BAG</button></div>
            <div class="hearticon">
              <img
                src="../assets/heart.png"
                width="25px"
                class="heart"
                alt=""
              />
            </div>
          </div>
        </div>
        <div class="forth">
          <div class="deleviry_time">Delivery by: Mar 07 - Mar 10</div>
          <div class="checkPincode">
            <strong><u>CHECK DETAILS</u></strong>
          </div>
        </div>
        <div class="fifth">
          <div class="d-flex justify-content-between" v-on:click="accordion(i )">
            <p class="bolds">PRODUCT DETAILS</p>
            <div class="iconacc">
              -
            </div>
          </div>
          <div :id="'panel' + i"  class="panel">
            <ul class="list">
              <li>65% viscose, 35% nylon</li>
              <li>Made in India</li>
              <li>Hand wash</li>
              <li>Unlined</li>
              <li>Pull-on styling with elastic drawstring waistband</li>
              <li>Shoulder cut-outs</li>
              <li>Ribbed knit fabric</li>
              <li>Revolve Style No. AAYR-WD5</li>
              <li>Manufacturer Style No. ATD4 F21</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
     <div class="similarproduct">
          <h3 class="similar">Similar Products</h3>
          <div class="slider_similar">
             <VueSlickCarousel :slidesToShow= 4 :slidesToScroll= 1 :arrows="true" :infinity="true" :speed="2000" >
                 <div v-for="(val, i) in productdetails.similar_products" :key="i" >
                   <!-- <img :src="val.image" alt="" /> -->
                   hello
                 </div>
            </VueSlickCarousel>
          </div>
      </div>

    <Footer />
  </div>
</template>

<script>
import VueSlickCarousel from "vue-slick-carousel";
import "vue-slick-carousel/dist/vue-slick-carousel.css";
// optional style for arrows & dots
import "vue-slick-carousel/dist/vue-slick-carousel-theme.css";
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";
import axios from "axios";

export default {
  name: "Product-View",
  components: {
    Header,
    Footer,
    VueSlickCarousel,
  },
  data() {
    return {
      URLParams: "",
      gallery: [],
      productdetails: {},
      size: [],
    };
  },
  created() {
    this.URLParams = this.$route.params.id;
    this.getData();
  },
  methods: {
    getData() {
      axios
        .get(
          `https://pim.wforwoman.com/pim/pimresponse.php/?service=product&store=1&url_key=${this.URLParams}`
        )
        .then((res) => {
          let result = res.data.result;
          this.gallery = result.gallery;
          this.productdetails = result;
          this.size = result.size;
          console.log(result.gallery);
        });
    },
  },
};
</script>

<style scoped>
.similarproduct{
  padding: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  flex-direction: column;
}
.similar{
  font-size: 24px;
  font-weight: 600;

}
.slider_similar{
  width: 90%;

}

.div{
  width: 90%;
  align-items: center;
  margin: 0px auto;
  display: flex;
  color: #565656;
  font-size: 12px;


}
.list{
  font-size: 12px;
  font-weight: 500;
}
.crumbs{
  font-weight: 500;
  color: black;
  margin-left: 5px;
}


.breadcrumbs{
  padding: 20px 0px;
  display: grid;
  grid-template-columns: 70% 30%;
}
.forth {
  font-size: 12px;
  display: flex;
  justify-content: space-between;
  font-weight: 500;
}
.custom-container {
  width: 100%;
}
.bolds{
  font-size: 12px;
  font-weight: 600;
}
.product-main {
  width: 100%;
  display: grid;
  grid-template-columns: 70% 30%;
}
.link{
  text-decoration: none;
  margin-right: 5px;
  color: #565656;
}
.productdetail {
  margin-right: 80px;
}
.topbox,
.second,
.third,
.forth,
.fifth {
  border-bottom: 1px #bebebe solid;
  padding: 20px 0px;
}
.heading {
  font-size: 16px;
  font-weight: 500;
}
.price {
  margin: 8px 0px;
  margin-bottom: 2px;
  font-size: 20px;
  font-weight: 500;
}
.discount {
  color: #eb0c0c;
}

.clickable {
  cursor: pointer;
}
.second {
  font-size: 13px;
}
.crosal{
  width: 90%;
  align-items: center;
  margin: 0px auto;


}
.crozalimg, .crozalimg img{
  width: 100%;
}
.mrp {
  color: #8a8a8a;
  font-size: 13px;
}
.variationImg img {
  width: 60px;
  margin: 10px;
  margin-left: 0px;
  cursor: pointer;
}
.variation {
  display: flex;
  flex-wrap: wrap;
}
.size {
  display: flex;
  justify-content: space-between;
  padding-top: 20px;
}
.sizes {
  display: flex;
  flex-wrap: wrap;
  padding: 20px 0px;
}
.sizelist {
  border: 1px solid rgb(182, 182, 182);
  border-radius: 10px;
  height: 42px;
  width: 42px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-right: 10px;
  margin-top: 10px;
  cursor: pointer;
}
.likebtns {
  padding: 9px 14px;
  border: 1px solid rgb(182, 182, 182);
  border-radius: 17px;
  font-size: 12px;
  margin-left: 10px;
}
.fitinfo,
.modals {
  display: flex;
  margin: 10px 0px;
  font-size: 12px;
  align-items: center;
  font-weight: 500;
}
.tobag {
  display: grid;
  grid-template-columns: 80% 20%;
  margin-top: 20px;
}
.bag {
  width: 100%;
  align-items: center;
  text-align: center;
  color: white;
  background-color: #000000;
  outline: none;
  border: none;
  padding: 18px 0px;
  border-radius: 8px;
}
.hearticon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
}
</style>
