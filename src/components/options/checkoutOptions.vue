<template>
  <div v-if="visibility" class="radioButtons" id="radioButtons">
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
      value="Authenticated"
      @input="chooseSettings"
    />
    Authenticated
    <input
      type="radio"
      id="standard"
      name="checkoutSolution"
      value="standard"
      @input="chooseSettings"
    />
    Standard
  </div>
</template>

<script>
export default {
  name: "checkoutOptions",
  props: ["settings", "instrument"],
  watch: {
    instrument: function (newVal) {
      this.visibility = newVal === "checkout" ? true : false;
    },
  },
  data() {
    return {
      visibility: false,
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
  float: left;
  width: auto;
  display: block;
}
</style>
