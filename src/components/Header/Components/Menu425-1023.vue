<template>
  <div>
    <div class="header"></div>
    <div class="wraper_burger-menu" @click="open()">
      <img
        class="burger-menu"
        src="@/assets/img/burger-menu.svg"
        alt="burger-menu"
        v-if="burgerMenu"
      />
      <img class="close-menu" src="@/assets/img/close.png" alt="close" v-else />
    </div>
    <div class="menu" v-if="!burgerMenu">
      <div class="el_level-1" v-for="(el, idx) in elements" :key="idx" :ref="idx">
        <h3>
          <a href="#">{{el.headings}}</a>
          <img
            class="arrow-close_level-2"
            src="@/assets/img/arrow-close.svg"
            alt="arrow-close"
            @click="openLevel2($event)"
            v-show="el.elLevel2"
          />
        </h3>
        <div class="wrapper-el_level-2">
          <ul class="el_level-2" v-for="(el, idx) in el.elLevel2" :key="idx">
            <h4>
              <a href="#">{{el.headings}}</a>
              <img
                class="arrow-close_level-3"
                src="@/assets/img/arrow-close.svg"
                alt="arrow-close"
                @click="openLevel3($event)"
                v-show="el.elLevel3"
              />
            </h4>
            <div class="wrapper-el_level-3">
              <li class="el_level-3" v-for="(el, idx) in el.elLevel3" :key="idx">
                <a href="#">{{el}}</a>
              </li>
            </div>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Menu",
  props: {
    elements: Array
  },
  components: {},
  data() {
    return {
      burgerMenu: true,
      flagCloseAllLevel2: "",
      flagCloseAllLevel3: ""
    };
  },
  methods: {
    open() {
      this.burgerMenu = !this.burgerMenu;
    },
    addClassOpen() {

      const elementWrapper = event.path[2].children[1];
      const elementArrow =  event.path[2].children[0].children[1];

      elementWrapper.classList.add("active");
      elementArrow.classList.add("rotate");

      event.toElement.scrollIntoView({ block: "start", behavior: "smooth" });
    },
    removeClassOpen() {

      const elementWrapper = event.path[2].children[1];
      const elementArrow =  event.path[2].children[0].children[1];

      elementWrapper.classList.remove("active");
      elementArrow.classList.remove("rotate");
    },
    removeAllClassOpen(elementWrapper, elementArrow) {
      document.querySelectorAll(elementWrapper).forEach(a => {
        a.classList.remove("active");
      });
      document.querySelectorAll(elementArrow).forEach(a => {
        a.classList.remove("rotate");
      });
    },
    openLevel2(event) {
      if (this.flagCloseAllLevel2 === "") {

        this.addClassOpen();
        this.flagCloseAllLevel2 = event.toElement;

      } else if (this.flagCloseAllLevel2 === event.toElement) {

        this.removeClassOpen();
        this.flagCloseAllLevel2 = "";

      } else {

        this.removeAllClassOpen(".wrapper-el_level-2", ".arrow-close_level-2");

        this.addClassOpen();
        this.flagCloseAllLevel2 = event.toElement;
      }
    },
    openLevel3(event) {
      if (this.flagCloseAllLevel3 === "") {

        this.addClassOpen();
        this.flagCloseAllLevel3 = event.toElement;

      } else if (this.flagCloseAllLevel3 === event.toElement) {

        this.removeClassOpen();
        this.flagCloseAllLevel3 = "";

      } else {

        this.removeAllClassOpen(".wrapper-el_level-3", ".arrow-close_level-3");

        this.addClassOpen();
        this.flagCloseAllLevel3 = event.toElement;
      }
    }
  }
};
</script>

<style lang="scss" scoped>
@import "@/styles/main.scss";

.header {
  width: 100%;
  height: 60px;
  background-color: $header-background-color;
  color: $header-color;
  position: fixed;
  z-index: 998;
}
.wraper_burger-menu {
  position: absolute;
  right: 0;
  margin: 20px;
  z-index: 999;
  position: fixed;
  .burger-menu {
    width: 20px;
  }
  .close-menu {
    width: 20px;
  }
}
.menu {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  width: 100%;
  height: auto;
  position: absolute;
  background-color: $menu-background-color;
  margin-top: 60px;
  .el_level-1 {
    cursor: pointer;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin: 10px;
    position: relative;
    a {
      text-decoration: none;
      color: $header-color;
    }
    h3 {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-family: "OpenSans-light";
    }
    .wrapper-el_level-2 {
      display: none;
      flex-direction: column;
      justify-content: center;
      .el_level-2 {
        padding: 8px 12px;
        h4 {
          display: flex;
          justify-content: space-between;
          align-items: center;
          width: 97%;
          font-family: "OpenSans-light";
        }
        .wrapper-el_level-3 {
          display: none;
          flex-direction: column;
          justify-content: center;
        }
        li {
          list-style-type: none;
          margin-top: 10px;
        }
        .el_level-3 {
          padding: 0px 12px;
          font-family: "OpenSans-light";
        }
        .active {
          display: flex;
        }
      }
    }
    .arrow-close_level-2,
    .arrow-close_level-3 {
      width: 20px;
      height: 20px;
      background-color: aliceblue;
      right: 0;
      margin-right: 12px;
      scroll-margin-top: 65px;
    }
    .active {
      display: flex;
    }
    .rotate {
      transform: rotate(180deg);
    }
  }
}
</style>
