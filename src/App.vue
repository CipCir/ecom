<template>
  <div id="app">
    <div v-if="isWrongOrientation" id="mainContainer">
      <WrongOrientation
        :defaultOrientation="inputObj.Orientation"
        :errorString="inputObj.errorOrientation"
      />
    </div>
    <div v-else id="appContent">
      <Single v-if="version=='single'" :inputObj="inputObj" :isMobile="isMobile" />
    </div>
  </div>
</template>

<script>
import Single from "./components/Single.vue";
import WrongOrientation from "./components/wrongOrientation.vue";

export default {
  name: "app",
  components: {
    Single,
    WrongOrientation
  },
  data() {
    return {
      inputObj,
      version: "single",
      currentOrientation: "",
      isWrongOrientation: false,
      isMobile: false
    };
  },
  created() {
    // resize listeners and orientation
    window.addEventListener("resize", this.checkOrientation);
    this.checkOrientation();
  },
  methods: {
    checkOrientation: function() {
      // if (typeof window.orientation !== 'undefined') {
      if (window.matchMedia("(orientation: portrait)").matches) {
        this.currentOrientation = "Portrait";
      } else if (window.matchMedia("(orientation: landscape)").matches) {
        this.currentOrientation = "Landscape";
      }

      if (this.currentOrientation !== this.inputObj.Orientation) {
        this.isWrongOrientation = true;
      } else {
        this.isWrongOrientation = false;
      }
      if (window.innerWidth < 768) {
        this.isMobile = true;
      } else {
        this.currentOrientation = "Desktop";
        this.isWrongOrientation = false;
        this.isMobile = false;
      }
      // } else {
      // 	this.currentOrientation = 'Desktop'
      // 	this.isWrongOrientation = false
      // 	this.isMobile = false
      // }
    }
  }
};
</script>

<style>
</style>
