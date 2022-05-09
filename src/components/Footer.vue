<template>
  <div class="footer">
    <div class="mainfooter">
      <div class="footer-top">
        <div class="img">
          <img src="../assets/logo2x.png" alt="" />
        </div>

        <div>
          <p class="text">
            Being Human Clothing was founded in 2012 to further the objective of
          </p>
          <p class="text">
            Being Human -The Salman Khan Foundation, a charitable trust devoted
            to education and healthcare initiatives for the
          </p>
          <p class="text">underserved population in India.</p>
          <p class="text-mobile">
            Being Human Clothing was founded in 2012 to further the objective of
            Being Human -The Salman Khan Foundation, a charitable trust devoted
            to education and healthcare initiatives for the underserved
            population in India.
          </p>
          <p class="bold click">Read More</p>
        </div>
      </div>
      <div class="footer-bottem">
        <div class="footer-widget">
          <div>
            <p class="bold2">ABOUT</p>
            <p class="footer-text">About Us</p>
            <p class="footer-text">Store Locator</p>
            <p class="footer-text">Career</p>
            <p class="footer-text">Become a partner</p>
            <p class="footer-text">Contact Us</p>
            <p class="footer-text">Blog</p>
          </div>
          <div>
            <p class="bold2">SUPPORT</p>
            <p class="footer-text">Privacy Policy</p>
            <p class="footer-text">Shipping Policy</p>
            <p class="footer-text">Return / Exchange Policy</p>
            <p class="footer-text">Track Order</p>
            <p class="footer-text">Return & Exchange</p>
          </div>
        </div>

        <div class="footer-search">
          <div class="search">
            <div class="input">
              <input type="text" placeholder="Enter your email id.." />
            </div>
            <div class="submit">Submit</div>
          </div>
          <div class="icon">
            <i class="space fa-brands fa-facebook-f"></i>
            <i class="fa-brands fa-instagram"></i>
            <i class="fa-brands fa-twitter"></i>
          </div>
        </div>
        <div class="footer-widget-mobile">
          <div class="footerspace">
            <div class="bold2" v-on:click="footeraccoudion(1)">ABOUT <span id="accfooter1">+</span></div>
            <div class="panel" id="footer-w-1">
              <p class="footer-text">About Us</p>
              <p class="footer-text">Store Locator</p>
              <p class="footer-text">Career</p>
              <p class="footer-text">Become a partner</p>
              <p class="footer-text">Contact Us</p>
              <p class="footer-text">Blog</p>
            </div>
          </div>
          <div class="footerspace">
            <div class="bold2" v-on:click="footeraccoudion(2)">SUPPORT <span id="accfooter2">+</span></div>
            <div class="panel" id="footer-w-2">
              <p class="footer-text">Privacy Policy</p>
              <p class="footer-text">Shipping Policy</p>
              <p class="footer-text">Return / Exchange Policy</p>
              <p class="footer-text">Track Order</p>
              <p class="footer-text">Return & Exchange</p>
            </div>
          </div>
        </div>
      </div>
      <div class="footerlast">
        <div class="f-img"><img src="https://www.libertyshoesonline.com/pub/media/wysiwyg/home/GreenHonchos-Logo.svg" alt=""></div>
        <div class="f-text">Copyright © 2022 Being Human Clothing. All rights reserved</div>
        <div></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Top-Footer",
  methods:{
    footeraccoudion(id){
      let panel = document.getElementById("footer-w-" + id);
       let icon = document.getElementById("accfooter" + id)
      if (panel.style.display === "block") {
        panel.style.display = "none";
        icon.innerText="+"

      } else {
        panel.style.display = "block";
        icon.innerText="-"
        
      }
    }
  }
};
</script>

<style scoped>
.footer-widget-mobile {
  display: none;
}
.img img {
  width: 200px;
  margin: 30px 0px;
}
.click{
  cursor: pointer;
}

.footer {
  display: grid;
  width: 100%;
  grid-template-columns: 90%;
  justify-content: center;
}
.mainfooter {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.footer-top {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  margin-bottom: 20px;
}
.text-mobile {
  display: none;
  font-size: 14px;
  word-spacing: 1.5px;
  margin: 10px 0px;
  max-width: 800px;
  align-self: center;
}
.text {
  font-size: 14px;
  word-spacing: 1.5px;
  margin: 10px 0px;
}
.bold {
  font-weight: 600;
}
.bold2 {
  font-weight: 500;
}
.footer-bottem {
  border-bottom: 1px solid black;
  border-top: 1px solid black;
  padding: 40px 0px;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  column-gap: 100px;
}
.footer-widget {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
}
.footer-text {
  margin: 20px 0px;
  font-size: 14px;
  word-spacing: 1.5px;
}
.footerlast{
  display: grid;
  grid-template-columns: 20% 60% 20%;
  align-items: center;
}
.footer-search {
  display: flex;
  flex-direction: column;
}
.search {
  display: grid;
  grid-template-columns: 70% 30%;
}
.submit {
  background-color: black;
  color: #ffcb05;
  padding: 20px 0px;
  text-align: center;
}
.input {
  background-color: white;
  display: flex;
  justify-content: center;
  align-items: center;
}
.input input {
  outline: none;
  width: 80%;
  border: none;
}
.f-text{
  text-align: center;
  align-items: center;
  
}
.input input::placeholder {
  font-style: italic;
  color: rgba(128, 128, 128, 0.596);
}
.icon svg {
  margin-right: 10px;
  color: #ffcb05;
  background-color: black;
  padding: 15px;
  font-size: 18px;
  border-radius: 50px;
}
.space {
  padding: 15px 18px !important;
}
.icon {
  margin-top: 30px;
}
@media screen and (max-width: 780px) {
  .footer-widget-mobile {
    display: grid;
  }
  #accfooter1, #accfooter2{
    float: right;
    font-size: 20px;
  }
  .text {
    display: none;
  }
  .text-mobile {
    display: block;
  }
  .bold {
    font-size: 12px;
  }
  .bold2 {
    font-weight: 700;
  }
  .footer-bottem {
    display: flex;
    flex-direction: column;
  }
  .footer-widget {
    display: none;
  }
  .footer {
    grid-template-columns: 100%;
  }
  .icon {
    display: flex;
    justify-content: center;
    margin-top: 0px;
    padding: 20px 0px;
    border-bottom: 1px solid #9b9b9b;
    border-top: 1px solid #9b9b9b;
  }
  .footerlast{
    display: flex;
    /* flex-direction: column; */
    justify-content: space-evenly;
}
.footerlast .f-img{
  width: 50%;

}
 .footerlast .f-text{
  font-size: 12px;

}
 .search {
    padding: 20px 0px;
  }
  .img img {
    width: 100px;
    margin: 10px;
  }
  .footer-bottem {
    padding: 0px 0px;
    border-top: 1px solid #9b9b9b;
  }
  .panel {
    display: none;
    overflow: hidden;
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
  .footerspace{
    padding: 20px;
    border-bottom: 1px solid #9b9b9b;
  }
}
</style>
