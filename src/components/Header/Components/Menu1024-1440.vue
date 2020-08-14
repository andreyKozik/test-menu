<template>
  <div class="menu">
    <div
      class="el_level-1"
      v-for="(el, idx) in elements"
      :key="idx"
      :ref="idx"
      v-on:mouseover="isActive($refs, idx)"
      v-on:mouseleave="notActive($refs, idx)"
    >
      <h4>
        <a href="#">{{el.headings}}</a>
      </h4>
      <div class="marker"></div>
      <div class="wrapper" v-show="el.elLevel2">
        <ul class="el_level-2" v-for="(el, idx) in el.elLevel2" :key="idx">
          <h4>
            <a href="#">{{el.headings}}</a>
          </h4>
          <li class="el_level-3" v-for="(el, idx) in el.elLevel3" :key="idx">
            <a href="#">{{el}}</a>
          </li>
        </ul>
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
    return {};
  },
  methods: {
    isActive: (refs, idx) => {

      const elementWrapper = refs[idx][0].children[1];
      const elementArrow = refs[idx][0].children[2];

      elementWrapper.classList.add("active");
      elementArrow.classList.add("active");
    },
    notActive: (refs, idx) => {

      const elementWrapper = refs[idx][0].children[1];
      const elementArrow = refs[idx][0].children[2];

      elementWrapper.classList.remove("active");
      elementArrow.classList.remove("active");
    }
  }
};
</script>

<style lang="scss" scoped>
@import "@/styles/main.scss";

.menu {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 600px;
  height: 100%;
  position: relative;
  margin: 0 5%;
  background-color: $header-background-color;
  font-family: "OpenSans-light";
  a {
    text-decoration: none;
    color: $header-color;
  }
  .el_level-1 {
    cursor: pointer;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    .marker {
      display: none;
      position: absolute;
      background-color: $marker;
      width: 77px;
      height: 5px;
      bottom: 0;
    }
    .wrapper {
      display: none;
      position: absolute;
      width: 150%;
      height: auto;
      background-color: $menu-background-color;
      margin: 60px 0px 0 -3%;
      top: 0;
      left: 0;
      justify-content: flex-start;
      padding: 0px 10px;
      .el_level-2 {
        padding: 20px;
        li {
          font-family: "OpenSans-light";
          list-style-type: none;
          margin-top: 10px;
        }
      }
    }
    .active {
      display: flex;
    }
  }
}
</style>