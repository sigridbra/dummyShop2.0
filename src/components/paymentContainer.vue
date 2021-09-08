<template>
  <div id="iframeContainers">
    <div class="checkin" id="checkinContainer">
    </div>
  <div id="showButton">
      <button
        :style="{ visibility: showOpenMenuButton ? 'visible' : 'hidden' }"
        id="openMenu"
        @click="openMenu"
      >
        open payment menu
      </button>
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
      if (newState === true && oldState === false) this.openPayment();
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
      showOpenMenuButton: false,
    };
  },
  methods: {
    openPayment() {
      let container =
        this.instrument === "checkout"
          ? this.checkoutContainer
          : this.paymentContainer;
      let setting = this.setting === "standard" ? "checkin" : null;
      //eslint-disable-next-line
      payex.hostedView[this.instrument](container).open(setting);
    },
    updateContainer(checkoutType) {
      this.showOpenMenuButton = false;
      switch (checkoutType) {
        case "MAC":
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
            onShippingDetailsAvailable: () => {
              this.showOpenMenuButton = true;
            },
          };
          break;
        }
      }
    },
    openMenu() {
      //eslint-disable-next-line
      payex.hostedView[this.instrument](this.checkoutContainer).open(
        "paymentmenu"
      );
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
.checkin {
  position: flex;
  clear: both;
}
</style>
