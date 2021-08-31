<template>
  <div id="body">
    <scriptInputs 
      :instrument="instrument"
      @onUpdateInstrument="instrument=$event"
      @onScriptAppend="openMenu()"
    />
    <paymentContainer 
      :instrument="instrument" 
    />
  </div>
</template>

<script>
import paymentContainer from "./paymentContainer.vue";
import ScriptInputs from "./scriptInputs.vue";

export default {
  name: "Body",
  data() {
      return {
          instrument: "no instrument",
      }
  },
  components: {
    ScriptInputs,
    paymentContainer,
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
