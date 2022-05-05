 <template>
  <div class="MainBox">
    <div class="maintop">
      <div class="topfilter">
        <div class="list">
          <strong>{{ name }}</strong
          >( {{ count }} )
        </div>
        <div class="sort">
          Sort by:
          <select
            class="dropdown"
            name="sort"
            v-on:change="changesort"
            id="sort"
          >
            <option v-for="(val, i) in sort" :key="i" :value="val.code">
              {{ val.label }}
            </option>
          </select>
        </div>
      </div>
    </div>
    <div class="box">
      <div id="category" class="category">
        <div v-if="filterprod.length !== 0" class="filters flex2">
          <div class="filterheading">Applied Filters</div>
          <div class="app-filters">
            <div class="appliedfilter" v-for="(val, i) in filterprod" :key="i">
              <div class="btn btn-secondary btn-size" v-on:click="removefilter(i)">{{ val.value }} <i class="fa-solid fa-xmark"></i></div>
              
            </div>
          </div>
           <div v-on:click="clearallfilter()" class="btn-size btn btn-danger">
              Clear all
            </div>
        </div>
        <div v-for="(val, i) in filter" :key="i" class="filters">
          <div class="flex" v-on:click="accordion(i)">
            <p>{{ val.filter_lable }}</p>
            <img
              src="../assets/arrow.png"
              :id="'acc' + i"
              height="10px"
              width="15px"
              alt=""
            />
          </div>
          <div :id="'panel' + i" class="panel">
            <div v-for="(val2, i2) in val.options" :key="i2" class="options"  >
              <input
                :id="val2.value_key"
                type="checkbox"
                class="color"
                :checked="checkedState(val2.value)"
                v-if="val2.code === 'color'"
                :style="{ backgroundColor: val2.value_key }"
                v-on:click="filterproduct(val2)"
              />
              <label v-else-if="val2.code === 'size'" v-on:click="filterproduct(val2)" class="text" for=""><div class="sizeboxes" v-if="!checkedState(val2.value)">{{ val2.value }}</div>
              <div class="sizebold sizeboxes" v-else>{{ val2.value }}</div>
              </label>

              <input
                :id="val2.value_key"
                type="checkbox"
                class="checkboxes"
                :checked="checkedState(val2.value)"
                v-else
                v-on:click="filterproduct(val2)"
              />
              <label
                v-if="val2.code !== 'size'"
                :for="val2.value_key"
                class="text"
                >{{ val2.value }}</label
              >
            </div>
          </div>
        </div>
      </div>
      <div v-if="loader" class="loader">
        <div class="spinner-border" role="status">
          <span class="sr-only">Loading...</span>
        </div>
      </div>

      <div id="products" v-else class="products">
        <div class="product" v-for="(val, i) in products" :key="i">
          <img :src="val.image" class="img" width="100%" alt="" />
          <div class="hiddenboxes">
            <div class="addwish">Add to Wishlist</div>
            <p class="text2">
              Size
              <span
                class="sizes"
                v-for="(val2, i) in sizes(val.size)"
                :key="i"
                >{{ val2.slice(1, val2.length - 1) }}</span
              >
            </p>
            <p class="text2">{{ val.name }}</p>
            <p class="text2">Rs. {{ val.price }}</p>
          </div>
          <div class="boxes">
            <div class="mobile_text">
              <div>
                <p class="text">{{ val.name }}</p>
                <p class="text">Rs. {{ val.price }}</p>
              </div>
              <img
                src="../assets/heart.png"
                width="15px"
                class="hearticon"
                alt=""
              />
            </div>
            <p class="text web_text">{{ val.name }}</p>
            <p class="text web_text">Rs. {{ val.price }}</p>
          </div>
        </div>
      </div>
      <div v-if="loader2" class="center web">
        
      </div>
      <div v-if="loader2" class="web center" >
        <div class="spinner-border" role="status">
          <span class="sr-only">Loading...</span>
        </div>
      </div>
      <div id="sorts" class="mobilesort">
        <div class="flex-d center py-3 border-bottom">
Sort by:
        </div>
          

            <div v-for="(val, i) in sort" :key="i" class="w-100" v-on:click="changesortinmobile(val.code)">

            <div v-if="val.code!==selectSort2" class="flex-d center py-3 border-bottom" >{{ val.label }}</div><div v-else class="flex-d center py-3 border-bottom custom-bg"><strong>{{ val.label }}</strong></div>
            </div>

        </div>
      <div class="mobile-filter">
        <div class="filterbutton">
          <div class="sort-mobile" v-on:click="mobileSort">
            <i class="fa-solid fa-arrow-right-arrow-left"></i> SORT
          </div>
          <div class="filter-mobile" v-on:click="mobileFilter">
            <i class="fa-solid fa-sliders"></i> FILTER
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Main-Box",
  data() {
    return {
      products: [],
      filter: [],
      count: 0,
      name: "",
      filterprod: [],
      filterlist:[],
      sort: [],
      selectSort: "",
      selectSort2: "",
      order: "desc",
      loader: false,
      loader2: false,
      page: 0,
    };
  },
  destroyed() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  mounted() {

    let filter=this.$route.params.filter
    let selectsort=this.$route.params.sortby
    if (filter?.length!==0 || selectsort?.length!==0) {
      // let filter=this.$route.params.filter
      // this.selectSort=this.$route.params.sortby
      console.log("with");
      this.getfilterproduct();
    }else{
      
      console.log("without");
    }
    this.getproduct();
    window.addEventListener("scroll", this.handleScroll);
  },
  methods: {
    // check if filter is active or not ( for the checkbox)
    checkedState(value_key){
      let filter=this.filterlist
      return filter.includes(value_key)
    },
    // remove the filters
    removefilter(i){
      let filters = this.filterprod;
      let filter=this.filterlist
      console.log(filter,"aa");
      filter.splice(i, 1)
      filters.splice(i, 1);
      this.filterlist= filter
      this.filterprod = filters;
      this.getfilterproduct();
    },
    // clear all filter
    clearallfilter(){
      this.filterlist=[]
      this.filterprod = [];
      this.getfilterproduct();
    },

    //Scroll Data load handling

    handleScroll() {
      // let product=document.getElementById("products")
      // if (   
      //   document.body.scrollHeight - 1500 <
      //   document.documentElement.scrollTop
      // ) {
      //   this.loadproduct(product.scrollHeight);
      // }
    },

    sizes(val) {
      let split_value = val.split(",");
      return split_value;
    },
    // For showing filter options in mobile
    mobileFilter() {
      let panel = document.getElementById("category");
      if (panel.style.display === "block") {
        panel.style.display = "none";
      } else {
        panel.style.display = "block";
      }
    },
    // For showing Sort option in mobile
    mobileSort() {
      let panel = document.getElementById("sorts");
      if (panel.style.display === "block") {
        panel.style.display = "none";
      } else {
        panel.style.display = "block";
      }
    },
    // Filters accordion function
    accordion(i) {
      let panel = document.getElementById("panel" + i);
      if (panel.style.display === "block") {
        panel.style.display = "none";
        document.getElementById("acc" + i).style.transform = "rotate(0deg)";
      } else {
        panel.style.display = "block";
        document.getElementById("acc" + i).style.transform = "rotate(180deg)";
      }
    },
    // Sort by function web
    changesortinmobile(val){
      if (val == "selling_price_high") {
        this.selectSort = "selling_price";
        this.order = "desc";
      } else if (val == "selling_price_low") {
        this.selectSort = "selling_price";
        this.order = "asc";
      } else {
        this.selectSort = val;
        
        this.order = "desc";
      }
      document.getElementById("sorts").style.display="none"
      this.selectSort2=val;
      this.getfilterproduct();
    },
     // Sort by function mobile
    changesort() {
      let val = document.getElementById("sort").value;
      this.selectSort2=val;
      if (val == "selling_price_high") {
        this.selectSort = "selling_price";
        this.order = "desc";
      } else if (val == "selling_price_low") {
        this.selectSort = "selling_price";
        this.order = "asc";
      } else {
        this.selectSort = val;
        this.order = "desc";
      }
      this.getfilterproduct();
    },
    // Main function to get the data on page load
    getproduct() {
      this.loader = true;
      axios
        .get(
          "https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=20&sort_by=&sort_dir=desc&filter="
        )
        .then((res) => {
          let result = res.data.result;
          this.products = result.products;
          this.filter = result.filters;
          this.count = result.count;
          this.name = result.name;
          let sort = [];
          for (let i = 0; i < result.sort.length; i++) {
            if (result.sort[i].code == "price") {
              sort.push(
                { code: "selling_price_low", label: "Low To High" },
                { code: "selling_price_high", label: "High To Low" }
              );
            } else {
              sort.push(result.sort[i]);
            }
          }
          this.sort = sort;
          this.page = 1;
          this.loader = false;
        });
    },
    // for creating the filter string
    filterproduct(cat) {
      let filters = this.filterprod;
      let filter=this.filterlist
      let check = 0;
      for (let i = 0; i < filters.length; i++) {
        if (cat.value == filters[i].value) {
          check = check + 1;
          filters.splice(i, 1);
          filter.splice(i, 1);
        }
      }
      if (check == 0) {
        filter.push(cat.value)
        filters.push(cat);
      }
      this.filterlist=filter
      this.filterprod = filters;
      this.getfilterproduct();
    },
    // for getting the filtered and sorted products
    getfilterproduct() {
      this.loader = true;
      let filters = this.filterprod;
      let filter = "";
      if (filters.length > 0) {
        for (let i = 0; i < filters.length; i++) {
          filter =
            filter +
            filters[i].code +
            "-" +
            filters[i].value.replaceAll(" ", "%2B") +
            ",";
        }
        filter = filter.replaceAll("&", "%26");
        filter = filter.substring(0, filter.length - 1);
      }
      axios
        .get(
          `https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=1&count=20&sort_by=${this.selectSort}&sort_dir=${this.order}&filter=${filter}`
        )
        .then((res) => {
          let result = res.data.result;
          this.products = result.products;
          this.count = result.count;
          this.name = result.name;
          this.page = 1;
          this.loader = false;
        });
    },
    // For loading the next page data
    loadproduct(productheight) {
      window.removeEventListener("scroll", this.handleScroll);
      this.loader2 = true;
      let filters = this.filterprod;
      let filter = "";
      if (filters.length > 0) {
        for (let i = 0; i < filters.length; i++) {
          filter =
            filter +
            filters[i].code +
            "-" +
            filters[i].value.replaceAll(" ", "%2B") +
            ",";
        }
        filter = filter.replaceAll("&", "%26");
        filter = filter.substring(0, filter.length - 1);
      }

      axios
        .get(
          `https://pim.wforwoman.com/pim/pimresponse.php/?service=category&store=1&url_key=top-wear-kurtas&page=${
            this.page + 1
          }&count=20&sort_by=${this.selectSort}&sort_dir=${
            this.order
          }&filter=${filter}`
        )
        .then((res) => {
          let result = res.data.result;
          this.products=this.products.concat(result.products);
          this.count = result.count;
          this.page = this.page + 1;
          this.name = result.name;

          window.scrollTo(0,productheight)
          this.loader2 = false;
          window.addEventListener("scroll", this.handleScroll);
        });
    },
  },
};
</script>

<style scoped>
.custom-bg{
  background-color: #d9d9d9;
}
p{
  margin-bottom: 0px;
}
.cross{
  outline: none;
  border: none;
}
.center{
  display: flex;
  justify-content: center;
  width: 100%;
}
.dropdown {
  background-color: transparent;
  outline: none;
  border: none;
}
.color {
  -webkit-appearance: none;
  cursor: pointer;
  appearance: none;
  font: inherit;
  color: transparent;
  width: 1.15em;
  height: 1.15em;
  border: 0.15em solid currentColor;
  border-radius: 50%;
}
.mobilesort{
  display: none;
}
.appliedfilter {
  /* padding: 5px; */
  margin: 5px;
  margin-top: 3px;
  /* border: 1px solid gray; */
  margin-left: 0px;
}
.color:checked {
  color: rgb(255, 255, 255); 
  border: 2px solid #1d1d1d;
  /* padding: 9px; */
}
.filterheading {
  margin: 10px 0px;
  font-size: 20px;
  font-weight: 500;
}
.sizeboxes{
  border: 1px solid #858585;
  justify-content: center;
  display: flex;
  align-items: center;
  height: 30px;
  width: 30px;
}
.btn-size{
  font-size: 14px;
}
.sizebold{
  font-weight: 600;
  border: 2px solid #858585;

}

.loader {
  width: 80%;
  display: flex;
  height: 80vh;
  position: fixed;
  bottom: 0px;
  justify-content: center;
  right: 0px;
  align-items: center;
}
.app-filters {
  display: flex;
  flex-wrap: wrap;
}
.mobile_text {
  display: none;
}
.checkboxes {
  height: 18px;
  width: 18px;
}
.maintop {
  display: flex;
  width: 100%;
  justify-content: center;
}
.size {
  -webkit-appearance: none;
  cursor: pointer;
  appearance: none;
  font: inherit;
  color: transparent;
  width: 1.15em;
  height: 1.15em;
  border: 0.15em solid currentColor;
  border-radius: 50%;
}
.size:checked {
  color: #000;
  font-size: 20px;
}
.appliedfilters {
  flex: 1;
  display: flex;
  flex-wrap: wrap;
}
.sort {
  font-size: 15px;
  color: #1d1d1d;
}
.flex {
  display: flex;
  justify-content: space-between;
  text-align: center;
  align-items: center;
  padding: 20px 20px 20px 40px;
}
.flex2 {
  padding: 20px 20px 20px 40px;
}
.img {
  cursor: pointer;
  margin-bottom: 10px;
}
.MainBox {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.addwish {
  margin: 25px;
  color: #858585;
  border: 1px solid #858585;
  text-align: center;
  margin-top: 30px;
  padding: 10px 0px;
  cursor: pointer;
}
.web_text {
  display: block;
}
.sizes {
  color: #858585;
  margin-right: 4px;
}
.box {
  width: 100%;
  display: grid;
  grid-template-columns: 20% 80%;
  border-top: 1px solid #d9d9d9;
}
.options {
  display: flex;
  flex-direction: row;
  margin: 10px 0px;
  align-items: center;
}
.options label {
  margin: 0px 18px;
}
.category {
  display: block;
}
.filters {
  cursor: pointer;
  border-right: 1px solid #d9d9d9;
  border-bottom: 1px solid #d9d9d9;
}
.products {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(min-content, max-content);
  margin-right: 20px;
}
.product {
  margin: 20px;
  position: relative;
}

.text {
  font-size: 14px;
  color: #747474;
}
.list {
  letter-spacing: 2px;
  word-spacing: 1.5px;
}
.topfilter {
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding: 25px 0px;
  margin: 0px 40px;
}
.text2 {
  font-size: 14px;
  margin: 5px 8px;
}
.panel {
  display: none;
  overflow: hidden;
  
  padding: 0px 0px 20px 40px;
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
.product:hover .hiddenboxes {
  display: block;
}
.hiddenboxes {
  display: none;
  position: absolute;
  bottom: 0;
  background-color: white;
  width: 100%;
  padding-bottom: 10px;
  box-shadow: 4px 4px 8px 0px rgba(161, 161, 161, 0.2);
}
.mobile-filter {
  display: none;
}
@media screen and (max-width: 1000px) {
  .products {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
  }
  .category {
    font-size: 12px;
  }
}
@media screen and (max-width: 780px) {
  .hiddenboxes {
    display: none;
  }
  .product:hover .hiddenboxes {
  display: none;
}
  .mobile_text {
    display: grid;
    position: relative;
    grid-template-columns: 80% 20%;
  }
  .mobile_text div {
    margin-left: 10px;
  }
  .web_text {
    display: none;
  }
  .web{
    display: none;
  }

  .products {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    column-gap: 20px;
    width: 100%;
    margin-right: 0px;
  }
  .product {
    margin: 10px 0px;
  }
  .box {
    position: relative;
    display: flex;
    border-top: none;
  }
  .topfilter {
    padding: 10px 0px;
  }
  .text {
    font-size: 13px;
  }
  .hearticon {
    position: absolute;
    top: 10px;
    right: 10px;
    width: 15px;
  }

  .category {
    position: fixed;
    display: none;
    z-index: 3;
    top: 0;
    left: 0;
    bottom: 60px;
    background-color: #f8f8f8;
    overflow-y: scroll;
    width: 70%;
  }
  .mobilesort{
    display: none;
    background-color: #f8f8f8;
    position: fixed;
    bottom: 60px;
    left: 0;
    z-index: 5;
    width: 100%;
  }
  .sort {
    display: none;
    background-color: #f8f8f8;
    position: fixed;
    bottom: 60px;
    left: 0;
    z-index: 5;
    width: 100%;
    padding: 20px;
  }
  .mobile-filter {
    height: 60px;
    background-color: black;
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .filterbutton {
    letter-spacing: 1.5px;
    width: 80%;
    font-size: 20px;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    color: #ffcb05;
    text-align: center;
  }
  .sort-mobile {
    border-right: 2px solid #ffcb05;
  }
  .sort-mobile svg {
    transform: rotate(90deg);
  }
  .loader {
    width: 10%;
    display: flex;
    height: 80vh;
    position: fixed;
    bottom: 0px;
    justify-content: center;
    right: 0px;
    align-items: flex-start;
  }
}
</style>
