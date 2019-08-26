<template>
  <div id="mainContainer">
    <div id="mainImgContainer">
      <div id="learn-btn" class="btn" @click="openModal()">Button</div>
      <img
        :src="(isMobile ? inputObj.imgs.path + inputObj.imgs.mainMobile : inputObj.imgs.path + inputObj.imgs.mainDesktop)"
      />
    </div>
    <!-- modal -->
    <div id="modalCont" v-if="ShowModal==true" class="background-modal" @click.self="closeModal()">
      <div class="modal_container container">
        <span class="close-button">
          <i class="fa fa-times-circle float-right" aria-hidden="true" @click="closeModal()"></i>
        </span>
        <span
          class="change-picture-button left"
          @click="updateimg('prev')"
          :class="{'disabled':ImgIndx==0}"
        >
          <i class="fa fa-chevron-left" aria-hidden="true"></i>
        </span>
        <span
          class="change-picture-button right"
          @click="updateimg('next')"
          :class="{'disabled':ImgIndx==this.inputObj.imgs.arrayDesktop.length-1}"
        >
          <i class="fa fa-chevron-right" aria-hidden="true"></i>
        </span>
        <div class="carousel">
          <img class="main-picture-carousel" :src="inputObj.imgs.path + mainImg " />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Single",
  props: {
    inputObj: Object,
    isMobile: Boolean
  },
  data() {
    return {
      mainImg: null,
      ImgIndx: 0,
      ShowModal: false
    };
  },
  created() {
    this.mainImg = this.inputObj.imgs.arrayDesktop[this.ImgIndx];
  },
  methods: {
    openModal() {
      $("body").addClass("noScroll");
      this.ShowModal = true;
    },
    closeModal() {
      $("body").removeClass("noScroll");
      this.ShowModal = false;
    },
    updateimg(dir) {
      let imgArr = this.inputObj.imgs.arrayDesktop;
      if (dir == "next") {
        if (this.ImgIndx < imgArr.length - 1) {
          this.ImgIndx++;
        }
      }
      if (dir == "prev") {
        if (this.ImgIndx > 0) {
          this.ImgIndx--;
        }
      }
      this.mainImg = this.inputObj.imgs.arrayDesktop[this.ImgIndx];
    }
  }
};
</script>

<style>
.noScroll {
  overflow: hidden;
}
</style>
<style scoped>
#learn-btn {
  /* position: absolute; */
  bottom: 2em;
  right: 2em;
}
.background-modal {
  width: 100%;
  height: 100%;
  background: rgba(128, 128, 128, 0.7490196078431373);
  position: fixed;
  z-index: 9999;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal_container {
  position: absolute;
  margin: auto;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  height: 90%;
  overflow-y: auto;
  background: #fff;
  border: 1px solid #dadada;
  border-radius: 0.25em;
  padding: 1em;
  box-shadow: 0 0 75px rgba(0, 0, 0, 0.35);
  background-color: #fff;
  z-index: 100001;
  margin-right: auto;
  margin-left: auto;
  padding-left: 3px;
  padding-right: 3px;
  min-width: 300px;
}
.close-button {
  display: block;
  position: absolute;
  width: 40px;
  height: 40px;
  right: 10px;
  text-align: center;
  z-index: 10000;
  cursor: pointer;
}
.close-button i {
  top: 0px !important;
  padding-top: unset !important;
  font-size: 2em;
  color: #666 !important;
}
.change-picture-button {
  display: block;
  position: absolute;
  width: 50px;
  top: 50%;
  transform: translateY(-50%);
  z-index: 99999;
  font-size: 3em;
  color: #666 !important;
  cursor: pointer;
}
.disabled {
  opacity: 0.65;
  cursor: initial;
}
.change-picture-button i {
  top: 0px !important;
  padding-top: unset !important;
  color: #666 !important;
}
.right {
  right: 0.25em;
}
.left {
  left: 0.25em;
}
.carousel {
  position: relative;
  min-height: 100%;
  display: flex;
  align-items: baseline;
  justify-content: center;
  overflow: hidden;
}
.main-picture-carousel {
  position: absolute;
  margin-top: 3em;
  margin: auto;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  max-width: 80%;
}
</style>
