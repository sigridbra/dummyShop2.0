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
      this.updateContainerName(newState);
    },
    eventOptions: function (newState) {
      this.updateEvent(newState)
    }
  },
  data() {
    return {
      container: {
        container: "paymentContainer",
        onPaymentCompleted: () => {
          this.paymentCompleted();
        }
      },
      showOpenMenuButton: false,
      showCompleteAlert: false
    };
  },
  methods: {
    openPayment() {
      let container = this.container;
      let setting = this.setting === "standard" ? "checkin" : null;
      //eslint-disable-next-line
      payex.hostedView[this.instrument](container).open(setting);
    },
    updateContainerName(checkoutType) {
      this.showOpenMenuButton = false;
      switch (checkoutType) {
        case "MAC":
        case "Authenticated": {
          this.container.container = {
              checkoutContainer: "paymentContainer",
          };
          break;
        }
        case "standard": {
          this.container.container = {
              checkinContainer: "checkinContainer",
              paymentMenuContainer: "paymentContainer",
            }
          break;
        }
      }
    },
    openMenu() {
      //eslint-disable-next-line
      payex.hostedView[this.instrument](this.container).open(
        "paymentmenu"
      );
    },
    closePayment() {
      //eslint-disable-next-line
      payex.hostedView[this.instrument]().close();
    },
    updateEvent(event) {
      let eventName = Object.getOwnPropertyNames(event);
      let eventEnabled = event[eventName];
      console.log(eventEnabled);
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
