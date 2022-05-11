<template>
  <div class="home">
    <Header />
    <MainBox/>
    <Footer space="true" />
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/components/Header.vue';
import MainBox from '@/components/MainBox.vue';
import Footer from '@/components/Footer.vue';
export default {
  name: 'HomeView',
  components: {
    Header,
    Footer,
    MainBox
  }
}
</script>
