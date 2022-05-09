<template>
  <div class="custom-container">
    <Header />
    <div class="breadcrumbs">
      <div class="div">
        <router-link to="/" class="link">Home</router-link> >
        <div class="crumbs">{{ productdetails.name }}</div>
      </div>
    </div>
    <div class="product-main">
      <div class="crosal">
        <VueSlickCarousel
          :slidesToShow="2"
          :slidesToScroll="1"
          :arrows="true"
          :infinity="true"
          :speed="3000"
          :autoplaySpeed="2000"
          :autoplay="true"
          :dots="true"
        >
          <div v-for="(val, i) in gallery" :key="i" class="crozalimg">
            <img :src="val.image" alt="" />
          </div>
        </VueSlickCarousel>
      </div>
      <div class="productdetail">
        <div class="topbox">
          <div class="heading">{{ productdetails.name }}</div>
          <div class="stars"></div>
          <div class="price">
            ₹{{ productdetails.selling_price }}
            <span
              v-if="productdetails.selling_price !== productdetails.price"
              class="discount"
              >{{ productdetails.discount }}% off</span
            >
          </div>
          <div
            v-if="productdetails.selling_price !== productdetails.price"
            class="mrp"
          >
            MRP:₹<strike>{{ productdetails.price }}</strike> (inclusive of all
            taxes)
          </div>
          <div v-else class="mrp">(inclusive of all taxes)</div>
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
            <div class="label">SIZE : {{ selectedsize }}</div>
            <strong><u>SIZE CHART</u></strong>
          </div>
          <div class="sizes">
            <div
              class="sizelist"
              v-for="(val, i) in size.split(',')"
              :key="i"
              v-on:click="selectsize(val.slice(1, val.length - 1))"
            >
              <strong v-if="val.slice(1, val.length - 1) === selectedsize">{{
                val.slice(1, val.length - 1)
              }}</strong>
              <span v-else>{{ val.slice(1, val.length - 1) }}</span>
            </div>
          </div>
          <div v-if="productdetails.fit" class="fitinfo">
            Fit info
            <div class="likebtns">{{ productdetails.fit }}</div>
          </div>
          <div v-if="productdetails.fit" class="modals">
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
          <div class="d-flex justify-content-between align-items-center" v-on:click="accordion(1)">
            <p class="bolds">PRODUCT DETAILS</p>
            <div id="iconacc1">+</div>
          </div>
          <div :id="'panel' + 1" class="panel">
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
        <div class="sixth">
          <div class="d-flex justify-content-between align-items-center" v-on:click="accordion(2)">
            <p class="bolds">PRODUCT DETAILS</p>
            <div id="iconacc2">+</div>
          </div>
          <div :id="'panel' + 2" class="panel">
            <div class="list2">
              <div
                class="attrib"
                v-for="(val, i) in productdetails.visible_attributes"
                :key="i"
              >
                <strong>{{ val.label }}</strong> : {{ val.value }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="similarproduct">
      <h3 class="similar">Similar Products</h3>
      <div class="slider_similar_web">
        <VueSlickCarousel
          :slidesToShow="4"
          :slidesToScroll="1"
          :arrows="true"
          :infinity="true"
          :speed="1500"
        >
          <div
            class="products"
            v-for="(val, i) in productdetails.bestseller_products"
            :key="i"
          >

             <router-link :to="{ path: val.url_key, params: { val: val.url_key } }" target="_blank" >
            <img :src="val.image" class="img" width="100%" alt=""/></router-link>
            <i class="fa-regular fa-heart heartq"></i>
            <div class="color"></div>
            <div class="text">
              {{ val.name }}
            </div>
            <div class="bottem_price">
              <div class="price2">
                ₹{{ val.selling_price }}
                <span v-if="val.selling_price !== val.price" class="mrp">
                  ₹<strike>{{ val.price }}</strike></span
                >
                <span v-if="val.selling_price !== val.price" class="discount">
                  {{ val.discount }}% off</span
                >
              </div>
            </div>
          </div>
        </VueSlickCarousel>
      </div>
      <div class="slider_similar_mobile">
        <VueSlickCarousel :slidesToShow="2" :slidesToScroll="1" :arrows="true" :infinity="true" :speed="1500"
        >
          <div class="products" v-for="(val, i) in productdetails.bestseller_products" :key="i" >

             <router-link :to="{ path: val.url_key, params: { val: val.url_key } }" target="_blank" >
            <img :src="val.image" class="img" width="100%" alt=""/></router-link>
            <i class="fa-regular fa-heart heartq"></i>
            <div class="color"></div>
            <div class="text">
              {{ val.name }}
            </div>
            <div class="bottem_price">
              <div class="price2">
                ₹{{ val.selling_price }}
                <span v-if="val.selling_price !== val.price" class="mrp">
                  ₹<strike>{{ val.price }}</strike></span
                >
                <span v-if="val.selling_price !== val.price" class="discount">
                  {{ val.discount }}% off</span
                >
              </div>
            </div>
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
      selectedsize: "L",
    };
  },
  created() {
    this.getData();
  },
  methods: {
     accordion(i) {
      let panel = document.getElementById("panel" + i);
     
      if (panel.style.display === "block") {
        panel.style.display = "none";
        document.getElementById("iconacc"+i).innerText = "+";
        
      } else {
        panel.style.display = "block";
        document.getElementById("iconacc"+i).innerText= "-";
        if(i===1){
        document.getElementById("panel2").style.display = "none";
        document.getElementById("iconacc2").innerText = "+";
        }else{
           document.getElementById("panel1").style.display = "none";
        document.getElementById("iconacc1").innerText = "+";
        }
      }
      
    },
    getData() {
      this.URLParams = this.$route.params.id;
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
    selectsize(id) {
      this.selectedsize = id;
    },
    customredirect(vals){
      this.$destroy();
      this.$router.push({ path: vals, params: { val: vals } })
       
    }
  },
};
</script>

<style scoped>
p{
  margin-bottom: 0;
}
.slider_similar_mobile{
  display: none;
}
.slider_similar_web {
  width: 90%;
  display: block;
}
.panel {
  display: none;
  overflow: hidden;

  /* padding: 0px 0px 20px 40px; */
}
.accordion {
  color: #444;
  cursor: pointer;
  padding: 18px;
  width: 100%;
  text-align: left;
  border: none;
  outline: none;
  transition: 5s;
}
.text {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  color: #8a8a8a;
  font-size: 13px;
  font-weight: 600;
  margin: 8px 0px;
}
.products {
  padding: 20px;
  width: 100%;
  position: relative;
}
.attrib {
  text-align: start;
  margin: 3px;
}
.heartq {
  position: absolute;
  top: 30px;
  right: 30px;
  color: rgb(51, 51, 51);
  font-size: 20px;
}
.similarproduct {
  padding: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  flex-direction: column;
}
.similar {
  font-size: 24px;
  font-weight: 600;
}


.div {
  width: 90%;
  align-items: center;
  margin: 0px auto;
  display: flex;
  color: #565656;
  font-size: 12px;
}
.list {
  font-size: 12px;
  font-weight: 500;
}
.list2 {
  font-size: 12px;
  font-weight: 500;
display: grid;
grid-template-columns: repeat(2, 1fr);
}
.crumbs {
  font-weight: 500;
  color: black;
  margin-left: 5px;
}

.breadcrumbs {
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
.bolds {
  font-size: 12px;
  font-weight: 600;
}
.product-main {
  width: 100%;
  display: grid;
  grid-template-columns: 70% 30%;
}
.link {
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
.fifth,
.sixth {
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
.price2 {
  margin: 8px 0px;
  margin-bottom: 2px;
  font-size: 16px;
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
.crosal {
  width: 90%;
  align-items: center;
  margin: 0px auto;
}
.crozalimg,
.crozalimg img {
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
@media screen and (max-width: 1040px) {

.product-main {
  width: 100%;
  display: grid;
  grid-template-columns: 60% 40%;
}
}
@media screen and (max-width: 768px) {
  .slider_similar_mobile{
    display: block;
    width: 90%;
  }
  .slider_similar_web{
    display: none;
  }
.product-main {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.productdetail{
  margin: 40px;
}
.breadcrumbs {
  padding: 20px 0px;
  display: grid;
  grid-template-columns: repeat(1, 1fr);
}
.similarproduct {
  padding: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  flex-direction: column;
}
}
</style>
