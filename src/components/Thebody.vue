<template>
  <div id="body">
    <scriptInputs
      :instrument="instrument"
      @onUpdateInstrument="instrument = $event"
      @onScriptAppend="scriptAppended()"
      @onSettingsUpdated="updateContainer($event)"
    />
    <paymentContainer
      :instrument="instrument"
      :isOpen="isOpen"
      :setting="setting"
    />
  </div>
</template>

<script>
import paymentContainer from "./paymentContainer.vue";
import ScriptInputs from "./scriptInputs.vue";

export default {
  name: "TheBody",
  data() {
    return {
      instrument: "",
      isOpen: false,
      setting: "",
    };
  },
  components: {
    ScriptInputs,
    paymentContainer,
  },
  methods: {
    scriptAppended() {
      this.isOpen = true;
    },
    updateContainer(setting) {
      this.setting = setting;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
