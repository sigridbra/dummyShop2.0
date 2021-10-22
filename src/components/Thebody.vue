<template>
  <div id="body">
    <scriptInputs
      :instrument="instrument"
      @onUpdateInstrument="instrument = $event"
      @onScriptAppend="scriptAppended()"
      @onSettingsUpdated="updateContainer($event)"
    />
    <PxEvents @onEventsUpdated="subscribedEvents = $event"/>
    <paymentContainer
      :instrument="instrument"
      :isOpen="isOpen"
      :setting="setting"
      :eventOptions="subscribedEvents"
    />
  </div>
</template>

<script>
import paymentContainer from "./paymentContainer.vue";
import ScriptInputs from "./scriptInputs.vue";
import PxEvents from "./options/pxEvents.vue";

export default {
  name: "TheBody",
  data() {
    return {
      instrument: "",
      isOpen: false,
      setting: "",
      subscribedEvents: {}
    };
  },
  components: {
    ScriptInputs,
    paymentContainer,
    PxEvents,
  },
  methods: {
    scriptAppended() {
      this.isOpen = true;
    },
    updateContainer(setting) {
      this.setting = setting;
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
