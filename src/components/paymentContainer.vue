<template>
  <div>
    <div class="checkin" id="checkinContainer">
      <button class="checkinButton" id="openMenu">open payment menu</button>
    </div>
    <div class="container" id="paymentContainer"></div>
  </div>
</template>

<script>
export default {
  name: "paymentContainer",
  props: ["instrument", "isOpen", "setting"],
  watch: {
    isOpen: function (newState, oldState) {
      if (newState === true && oldState === false) this.openMenu();
    },
    setting: function (newState) {
      this.updateContainer(newState);
    },
  },
  data() {
    return {
      checkoutContainer: {
        container: "paymentContainer",
      },
      paymentContainer: {
        container: "paymentContainer",
      },
    };
  },
  methods: {
    openMenu() {
      let container =
        this.instrument === "checkout"
          ? this.checkoutContainer
          : this.paymentContainer;
      //eslint-disable-next-line
      payex.hostedView[this.instrument](container).open();
    },
    updateContainer(checkoutType) {
      switch (checkoutType) {
        case "Authenticated": {
          this.checkoutContainer = {
            container: {
              checkoutContainer: "paymentContainer",
            },
          };
          break;
        }
        case "standard": {
          this.checkoutContainer = {
            container: {
              checkinContainer: "checkinContainer",
              paymentMenuContainer: "paymentContainer",
            },
          };
          break;
        }
        case "MAC": {
          this.checkoutContainer = {
            container: "paymentContainer",
          };
          break;
        }
      }
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
