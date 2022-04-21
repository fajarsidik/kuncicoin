<template>
  <div>
    <div class="flex justify-center align-center">
      <img class="logo" src="./assets/img/logo-kuncicoin.png">
    </div>
    <div class="flex justify-center">
      <div class="menu">
        <a @click="linkTo('/')">Assessment 1</a>
        <a @click="linkTo('/product')">Assessment 2</a>
      </div>
    </div>
      <app-router></app-router>
    

    
  </div>
</template>

<script>


import AppRouter from "./components/AppRouter";
export default {
  name: 'App',  
  components: {        
    AppRouter
  },
   methods: {
    linkTo(route) {
      window.location = route;
    }
  }
}
</script>

<style lang="scss" scoped>
  .logo{
    padding: 40px 0;
    max-width: 320px;
  }
  .menu{
    a{
      margin: 0 10px;
      cursor: pointer;
      padding-bottom: 5px;
      border-bottom: 1px dashed #ccc;
    }
    margin-bottom: 20px;
  }
</style>>

