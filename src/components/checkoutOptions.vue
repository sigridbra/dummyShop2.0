<template>
  <div class="radioButtons" id="radioButtons">
    <a>using view-checkout?</a><br />
    <input
      type="radio"
      id="MAC"
      name="checkoutSolution"
      value="MAC"
      @input="chooseSettings"
    />
    Merchant Authenticated
    <input
      type="radio"
      id="standard"
      name="checkoutSolution"
      value="standard"
      @input="chooseSettings"
    />
    Checkout Managed Payer
    <input
      type="radio"
      id="standard"
      name="checkoutSolution"
      value="Authenticated"
      @input="chooseSettings"
    />
    Authenticated checkout
  </div>
</template>

<script>
export default {
  name: "checkoutOptions",
  props: ["settings", "instrument"],
  watch: {
    instrument: function (newVal) {
      this.visibility = newVal === "checkout" ? "visible" : "hidden";
    },
  },
  data() {
    return {
      visibility: "hidden",
    };
  },
  methods: {
    chooseSettings(event) {
      this.$emit("onUpdateSettings", event.target.value);
    },
  },
};
</script>

<style scoped>
.radioButtons {
  visibility: v-bind(visibility);
  float: left;
  width: auto;
  display: block;
}
</style>
