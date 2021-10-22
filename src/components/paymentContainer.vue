<template>
  <div id="iframeContainers">
    <div class="checkin" id="checkinContainer"></div>
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
    <img
      src="https://media2.giphy.com/media/mJHSkWKziszrkcNJPo/giphy.gif"
      :style="{ visibility: showCompleteAlert ? 'visible' : 'hidden' }"
    />
  </div>
</template>

<script>
export default {
  name: "paymentContainer",
  props: ["instrument", "isOpen", "setting", "eventOptions"],
  watch: {
    isOpen: function (newState, oldState) {
      if (newState === true && oldState === false) this.openPayment();
    },
    setting: function (newState) {
      this.updateContainer(newState);
    },
    eventOptions: function (newState) {
      console.log(newState);
    }
  },
  data() {
    return {
      checkoutContainer: {
        container: "paymentContainer",
        onPaymentCompleted: () => {
          this.paymentCompleted();
        }
      },
      paymentContainer: {
        container: "paymentContainer",
        onPaymentCompleted: () => {
          this.paymentComplete();
        },
      },
      showOpenMenuButton: false,
      showCompleteAlert: false
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
            onPaymentPaid: () => {
              this.paymentComplete();
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
            onPaymentPaid: () => {
              this.paymentComplete();
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
    closePayment() {
      //eslint-disable-next-line
      payex.hostedView[this.instrument]().close();
    },
    // events
    paymentComplete() {
      this.closePayment();
      this.showCompleteAlert = true;
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
