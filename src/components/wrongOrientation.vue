<template>
  <div class="fullPage">
    <div class="container">
      <img
        class="info-img"
        :src="'https://cdn.ipsosinteractive.com/deploy/products/MCRT/app/img/' + (defaultOrientation === 'Landscape' ?  'rotateHoriz' : 'rotateVert') + '.png'"
      />
      <p class="info-string">{{ errorString }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "WrongOrientation",
  props: {
    defaultOrientation: String,
    errorString: String
  }
};
</script>

<style>
.fullPage {
  background-color: #fff;
  z-index: 100001;
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
}
.fullPage,
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.info-string {
  font-weight: bold;
  font-size: 1.5em;
  max-width: 90%;
}
.info-img {
  width: 40%;
  height: 50%;
}
</style>
