<template>
  <div class="head">
    <div class="top-head">
      <div></div>
      <div class="coupen top-p">
        ADDITIONAL 10% OFF ON ORDERS ABOVE RS.4999.USE CODE: PLUS10
      </div>
      <div class="login-secton top-p ">Help | Track Order | Login</div>
    </div>
    
    <div class="box">
      <div class="mainheader">
        <img src="../assets/logo.png" alt="" />
        <div class="nav">
          <a class="navlink" href="">NEW ARRIVALS</a>
          <a class="navlink" href="">MEN</a>
          <a class="navlink" href="">WOMEN</a>
          <a class="navlink" href="">ACCESSORIES</a>
          <a class="navlink" href="">SALE</a>
        </div>
        <div class="search d-flex"><div class="px-3">SEARCH</div>  BAG ( 0 )</div>
      </div>
    </div>
    <div class="box-mobile">
      <div class="mainheader">
        <div class="top">
          <div v-on:click="toogle" class="hamburger"><i class="fa-solid fa-bars" ></i></div>
          <img src="../assets/logo2x.png" width="60px" alt="" />
       
        <div class="search"><img src="../assets/heart.png" class="nav-img" alt=""><img src="../assets/user.png" class="nav-img" alt=""><img src="../assets/cart.png" class="nav-img" alt=""></div>
        </div>
        <div id="nav-main" class="nav-main">
          <div class="close"><div v-on:click="toogle"><i  class="fa-solid fa-xmark"></i></div></div>
          <div class="nav">
          <a class="navlink" href="">NEW ARRIVALS</a>
          <a class="navlink" href="">MEN</a>
          <a class="navlink" href="">WOMEN</a>
          <a class="navlink" href="">ACCESSORIES</a>
          <a class="navlink" href="">SALE</a>
          <div class="w-100 navlink">Help | Track Order | Login</div>
        </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Top-Header",
  created(){
    
  },
  methods:{
   
    toogle(){
      let panel = document.getElementById("nav-main");
          if (panel.style.display === "block") {
            panel.style.display = "none";
        } else {
            panel.style.display = "block";
            document.getElementById("sorts").style.display="none"
            document.getElementById("category").style.display="none"
        }
        
    },
    
  }
};
</script>

<style scoped>
.head {
  width: 100%;
  border-bottom: 1px solid #000;
}
.top-head {
  background-color: #231f20;
  color: #ffcb05;

  width: 100%;
  display: grid;
  grid-template-columns: 20% 60% 20%;
  text-align: center;
}
.top-p {
  margin: 10px 0px;
}
.login-secton {
  margin-right: 50px;
  text-align: right;
}
.mainheader {
  font-size: 15px;
  font-weight: 500;
  display: flex;
  align-items: center;
  width: auto;
}
.box {
  padding: 0px 60px;
  display: grid;
  grid-template-columns: 100%;
}
.nav {
  flex: 1;
}
.navlink {
  text-decoration: none;
  color: black;
  margin-left: 100px;
}
.box-mobile{
  display: none;
}
@media screen and (max-width: 1280px) {
  .top-head {
    display: flex;
    justify-content: space-evenly;
  }
  .navlink {
    margin-left: 50px;
  }
}
@media screen and (max-width: 1000px) {
  .top-head {
    font-size: 14px;
  }
  .navlink {
    font-size: 12px;
    margin-left: 20px;
  }
}
@media screen and (max-width: 780px) {
  .hamburger{
    width: 100%;
    
  }
  .box{
    display: none;
  }
  .top{
    display: grid;
    align-items: center;
    width: 100%;
    grid-template-columns: repeat(3,1fr);
    justify-items: center;
  }
  .top-head {
    font-size: 12px;
  }
  .login-secton {
    margin-right: 20px;
    display: none;
  }
  .navlink {
    font-size: 16px;
    width: 100%;
    padding: 20px 0px;
    border-right: 1px solid #d9d9d9;
  border-bottom: 1px solid #d9d9d9;
  margin-left: 0px;
  }
  .nav{
    display: flex;
    justify-content: center;
    width: 100%;
    text-align: center;
    flex-direction: column;
  }
  .nav-main{
    display: none;
    position: fixed;
     z-index: 100;
    top: 0;
    left: 0;
    bottom: 60px;
    background-color: #f8f8f8;
    
    width: 70%;
  }
  .box-mobile{
    align-items: center;
    padding: 0px 20px;
    display: grid;
    grid-template-columns: 100%;
  }
  .mainheader{
    display: flex;
    flex-direction: column;
  }
  .search{
    float: right;
        width: 100%;
    text-align: end;
  }
  .close{
    width: 100%;
    float: right;
    text-align: end;
    margin: 5px 20px;
    font-size: 20px;
  }
  .nav-img{
    width: 25px;
    margin-left: 10px;
  }
  .top svg{
    font-size: 26px;
  }
  .head{
    border-bottom: none;
  }
}
</style>
