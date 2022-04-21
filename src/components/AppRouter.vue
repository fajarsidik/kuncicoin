<!-- Router.vue -->
<template>
  <component :is="routedComponent"></component>
</template>


<script>
import Home from "../pages/Home.vue";
import ProductPage from "../pages/ProductPage.vue";

const routes = {
  "/": Home,
  "/product": ProductPage
};

export default {
  data() {
    return { current: window.location.pathname };
  },
  computed: {
    routedComponent() {
      return routes[this.current];
    }
  },
  render(createElement) {
    return createElement(this.routedComponent);
  }
};
</script>
