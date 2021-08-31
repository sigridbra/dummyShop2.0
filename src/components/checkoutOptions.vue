<template>
  <div>
    <div class="radioButtons" id="radioButtons">
      <a>using checkout?</a><br />
      <input type="radio" id="MAC" name="checkoutSolution" value="MAC" />
      Merchant Authenticated
      <input
        type="radio"
        id="standard"
        name="checkoutSolution"
        value="standard"
      />
      Checkout Managed Payer
      <input
        type="radio"
        id="standard"
        name="checkoutSolution"
        value="Authenticated"
      />
      Authenticated checkout
    </div>
  </div>
</template>

<script>
export default {
  name: "checkoutOptions",
  data() {
    return {
      settings: "",
    };
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