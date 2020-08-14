<template>
  <div id="app">
    <Header/>
  </div>
</template>

<script>
import { mapActions } from "vuex";

import Header from "@/components/Header/Header";

export default {
  components: {
    Header
  },
  methods: {
    ...mapActions({
      changeWindowWidth: "changeWindowWidth"
    }),
    listenerWindowWidth() {
      this.changeWindowWidth(window.innerWidth);
      window.addEventListener(
        `resize`,
        e => {
          this.changeWindowWidth(e.target.innerWidth);
        },
        false
      );
    }
  },
  mounted() {
    this.listenerWindowWidth();
  },
};
</script>

<style lang="scss">
  @import "@/styles/main.scss";

  @font-face {
    font-family: "Exo-medium";
    src: url("~@/assets/fonts/exo/Exo-Medium.ttf");
  }

  @font-face {
    font-family: "Exo-regular";
    src: url("~@/assets/fonts/exo/Exo-Regular.ttf");
  }


  @font-face {
    font-family: "OpenSans-light";
    src: url("~@/assets/fonts/open_sans/OpenSans-Light.ttf");
  }


  body {
    margin: 0;
    padding: 0;
  }
</style>
