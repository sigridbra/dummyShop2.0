<template>
  <div class="checkin" id="checkinContainer">
    <button class="checkinButton" id="openMenu">open payment menu</button>
  </div>
  <button v-on:click="openMenu" class="submit" id="submitButton">open</button>
  <div class="container" id="paymentContainer"></div>
</template>

<script>
export default {
  name: "paymentContainer",
  props: ["instrument", "checkoutVersion"],
  methods: {
    openMenu() {
      let container = {
        container: "paymentContainer",
      };
      if (this.instrument === "checkout") {
        container = {
          container: {
            checkoutContainer: "paymentContainer",
          },
          culture: "en-US",
        };
      }
      //eslint-disable-next-line
      payex.hostedView[this.instrument](container).open();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  display: block;
  position: relative;
  height: auto;
  width: auto;
}
.checkinButton {
  display: none;
}
.checkin {
  position: flex;
  clear: both;
}
</style>
