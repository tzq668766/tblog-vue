<template>
  <div id="app">
    <transition name="fade">
      <template v-if="preloading">
        <Preload />
      </template>
      <div v-if="!preloading">
        <Navbar></Navbar>
        <router-view></router-view>
        <Footer></Footer>
      </div>
    </transition>
  </div>
</template>

<script>
import Navbar from './components/Navbar'
import Footer from './components/Footer'
import Preload from './components/Preload'

export default {
  name: 'app',
  components: {
    Navbar,
    Footer,
    Preload,
  },
  data(){
    return{
        preloading: true,
    };
  },
  methods:{
      showLoader() {
          const app = this;
          setTimeout(() => {
              app.preloading = false;
          }, 3000);
      },
      boot() {
          this.showLoader();
      },
  },
  mounted(){
    this.boot();
  }
}
</script>

<style>
body{
  background-color: #e1e1e1;
  font-family: "Helvetica Neue","Luxi Sans","DejaVu Sans",Tahoma,"Hiragino Sans GB",STHeiti,sans-serif!important;
}
a{
  cursor: pointer;
}
#app {
  margin-top: 80px;
}
.panel {
  margin-bottom: 13px
}

.panel .header {
  padding: 10px;
  background-color: #f6f6f6;
  border-radius: 3px 3px 0 0
}

.panel .header.topic-header,.panel .inner {
  background-color: #fff
}

.panel .moon {
  padding: 10px
}

.panel .moon_tags {
  padding-left: 10px
}

.panel .inner {
  padding: 10px;
  border-radius: 0 0 3px 3px
}
.breadcrumb a {
  color: #80bd01;
}
.wrapper {
  margin: 20px 0;
  padding: 8px;
  background-color: white;
  border: 1px solid #DDD;
  border-radius: 4px;
  -webkit-border-radius: 4px;
  -moz-border-radius: 4px;
  -o-border-radius: 4px;
  -khtml-border-radius: 4px;
}
.errors{
  color:red;
  font-size:12px;
}
</style>
