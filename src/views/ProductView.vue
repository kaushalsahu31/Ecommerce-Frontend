<template>
  <div class="custom-container">
    <Header />
    <div class="breadcrumbs">
      <div class="div">
        <router-link to="/" class="link">Home</router-link> >
        <div class="crumbs">{{ productdetails.name }}</div>
      </div>
    </div>
    <div id="main" class="product-main">
      <div class="crosal">
        <div id="slider">

        
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
          
             <span id="show">VIP Club Member get an extra discount of Rs.60 and Free Shipping. <strong id="hidetext1" v-on:click="hide(true)" class="clickable">Read More</strong></span>
            <span id="hide">
             VIP Club Member get an extra discount of Rs.60 and Free Shipping. They can be styled in many ways with bottom-wear gilets or drapes.
            Be it a casual-day-look kurta or the one for the light occasion, W
            has it all. Get your favourite kurtas and style them the way you
            want. <strong id="hidetext2" v-on:click="hide(false)" class="clickable">Read less</strong>
            </span>
            
          
          
          
        </div>
        <div class="third">
          <div class="color">Colour : {{ productdetails.color }}</div>
          <div class="variation">
            <div
              v-for="(val, i) in colorVarient"
              :key="i"
              class="variationImg"

            >
              <img :src="val.image_url" v-if="productdetails.color==val.color_name" class="selectcolor bold" v-on:click="changecolor(val.color_name)"  alt="" />
              <img :src="val.image_url" class="selectcolor" v-else v-on:click="changecolor(val.color_name)"  alt="" />
              <img src="../assets/Selected.svg" v-if="productdetails.color==val.color_name" class="selectedicon" alt="">
              <img src="../assets/Selected.svg" v-else class="hideicon" alt="">
            </div>
          </div>
          <div class="size">
            <div class="label">SIZE : {{ selectedsize }}</div>
            <strong><u>SIZE CHART</u></strong>
          </div>
          <div class="sizes">
            <div
              
              v-for="(val, i) in size.split(',')"
              :key="i"
              v-on:click="selectsize(val.slice(1, val.length - 1))"
            >
              <div class="sizelist" v-if="val.slice(1, val.length - 1) === selectedsize">{{
                val.slice(1, val.length - 1)
              }}</div>
              <div class="sizelist2" v-else  >{{ val.slice(1, val.length - 1) }}</div>
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
          <div
            class="d-flex justify-content-between align-items-center paddings"
            v-on:click="accordion(1)"
          >
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
          <div
            class="d-flex justify-content-between align-items-center paddings"
            v-on:click="accordion(2)"
          >
            <p class="bolds">KNOW ABOUT PRODUCT</p>
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
        <div class="seventh">
          <div class="imput">
            <img src="../assets/location.svg" class="locationicon" alt="">
            <input placeholder="Enter delivery pincode" oninput="this.value = this.value.replace(/[^0-9.]/g, '').replace(/(\..*?)\..*/g, '$1');" inputmode="numeric"  id="check" type="text" maxlength="6" autocomplete="off" class="location" value="">

            <button class="button"><strong>check pincode</strong></button>
          </div>
        </div>
      </div>
    </div>
    <div class="similarproduct">
      <h3 class="similar">Best Seller Products</h3>
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
            <router-link
              :to="{ path: val.url_key, params: { val: val.url_key } }"
              target="_blank"
            >
              <img :src="val.image" class="img" width="100%" alt=""
            /></router-link>
            <i class="fa-regular fa-heart heartq"></i>
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
        <VueSlickCarousel
          :slidesToShow="2"
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
            <router-link
              :to="{ path: val.url_key, params: { val: val.url_key } }"
              target="_blank"
            >
              <img :src="val.image" class="img" width="100%" alt=""
            /></router-link>
            <i class="fa-regular fa-heart heartq"></i>
            <!-- <div class="color"><div class="colors">
              </div>
              <strong class="siz"><u>Sizes</u></strong>
              </div> -->
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
    <div v-if="productdetails.similar_products!==undefined" class="similarproduct">
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
            v-for="(val, i) in productdetails.similar_products"
            :key="i"
          >
            <router-link
              :to="{ path: val.url_key, params: { val: val.url_key } }"
              target="_blank"
            >
              <img :src="val.image" class="img" width="100%" alt=""
            /></router-link>
            <i class="fa-regular fa-heart heartq"></i>
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
        <VueSlickCarousel
          :slidesToShow="2"
          :slidesToScroll="1"
          :arrows="true"
          :infinity="true"
          :speed="1500"
        >
          <div
            class="products"
            v-for="(val, i) in productdetails.similar_products"
            :key="i"
          >
            <router-link
              :to="{ path: val.url_key, params: { val: val.url_key } }"
              target="_blank"
            >
              <img :src="val.image" class="img" width="100%" alt=""
            /></router-link>
            <i class="fa-regular fa-heart heartq"></i>

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

    <Footer space="true" />
  </div>
</template>

<script>
import VueSlickCarousel from "vue-slick-carousel";
import "vue-slick-carousel/dist/vue-slick-carousel.css";
// optional style for arrows & dots    display: flex;
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
      colorVarient: [
        {
          image_url: "https://wforwoman.gumlet.io/product/21AUW16786-117537/665/21AUW16786-117537_1.JPG",
          color_name: "Blue"
        },
        {
          image_url: "https://wforwoman.gumlet.io/product/21AUW16783-117388/665/21AUW16783-117388.jpg",
          color_name: "Pink"
        },
        {
          image_url: "https://wforwoman.gumlet.io/product/20AUW13770-114732/665/20AUW13770-114732_1.JPG",
          color_name: "Black"
        }
      ],
    };
  },
  created() {
    this.getData();
    // window.addEventListener("scroll", this.handleScroll);
  },
//   destroyed(){
// window.removeEventListener("scroll", this.handleScroll);
//   },
  methods: {
    changecolor(val){
      this.productdetails.color=val
    },
    // handleScroll(){
    //   let slider = document.getElementById("slider")
    //   console.log(slider); 
    //   // if (this.$refs.input.height< this.$refs.main.height-100 ) {
        
    //   // }
      
    // },
    
    accordion(i) {
      let panel = document.getElementById("panel" + i);

      if (panel.style.display === "block") {
        panel.style.display = "none";
        document.getElementById("iconacc" + i).innerText = "+";
      } else {
        panel.style.display = "block";
        document.getElementById("iconacc" + i).innerText = "-";
        if (i === 1) {
          document.getElementById("panel2").style.display = "none";
          document.getElementById("iconacc2").innerText = "+";
        } else {
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
    customredirect(vals) {
      this.$destroy();
      this.$router.push({ path: vals, params: { val: vals } });
    },
    hide(id){
      if(id){
        document.getElementById("hide").style.display="block"
        document.getElementById("show").style.display="none"

        

      }else{
        document.getElementById("show").style.display="block"
        document.getElementById("hide").style.display="none"

      }
      
    }
    
       
    
  },
};
</script>

<style scoped>
.locationicon{
  width: 13px;
}
.variationImg{
  position: relative;
}

.bold{
 
  border: 2px solid black;
}
.smooth{
  color: white;
  background-color: #000000;
}
.selectedicon{
  width: 13px !important;
  height: 13px;
  position: absolute;
  top: 4px;
  right: 4px;
  z-index: 11;
}
.hideicon{
  display: none;

}

#hide {
display: none;
  
}
.color {
  display: flex;
  justify-content: space-between;
  font-size: 12px;
}
p {
  margin-bottom: 0;
}
.slider_similar_mobile {
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


.location{
  border: none;
  outline: none;
  font-size: 12px;
  background: transparent;
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
.imput{
  padding: 17px 0px;
  border-radius: 10px;
  align-items: center;
  /* margin: 0px 10px; */
  width: 100%;
  display: flex;
  justify-content: space-evenly;
  background-color: #ECECEC;
}
.button{
  outline: none;
  background: none;
  font-size: 12px;
  border: none;
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
.seventh {
  border-bottom: 1px #DFDFDF solid;
  padding: 20px 0px;
}
.fifth,
.sixth{
    border-bottom: 1px #DFDFDF solid;
  
}
.paddings{
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
.sizelist2{
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
.sizelist {
  border: 1px solid rgb(182, 182, 182);
  border-radius: 10px;
  background-color: black;
  color: white;
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

  .crosal {
  width: 85%;
}
  .list2 {
  grid-template-columns: repeat(1, 1fr);
}
  .slider_similar_mobile {
    display: block;
    width: 90%;
  }
  .slider_similar_web {
    display: none;
  }
  .product-main {
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  .productdetail {
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
  .tobag{
    position: fixed;
    bottom: 0px;
    left: 0px;
    right: 0px;
    width: 100%;
    background-color: #F8F8F8;
    z-index: 20;
    border-top: 1px solid #DFDFDF;
  padding: 10px;
  }
}
</style>
