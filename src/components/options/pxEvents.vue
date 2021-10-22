<template>
<button class="openEventMenu" @click="showEventOptions">events</button>
  <div v-if="showEvents" id="pxEventHandler" class="pxEventHandler">
    <div class="fullForm" v-for="(value, key, index) in events" :key="index">
      <label :for="key">
        <input type="checkbox" :id="key" v-model="events[key]" />
        {{ key }}
      </label>
    </div>
    <button @click="submitEvents">submit</button>
  </div>
</template>


<script>
export default {
  name: "pxEvents",
  emits: ["onEventsUpdated"],
  data() {
    return {
      showEvents: false,
      events: {
        onPaymentCompleted: false,
        onPaymentPaid: false,
        onEventNotification: false,
        onInstrumentSelected: false,
        onExternalRedirect: false,
        onError: false,
        onTermsOfServiceRequested: false,
        onOutOfViewRedirect: false,
        OnApllicationConfigured: false,
        onPaymentAborted: false,
        onPaymentFailed: false,
        ExternalOpen: false,
        onOutOfViewOpen: false,
      },
    };
  },
  methods: {
      showEventOptions() {
          this.showEvents = this.showEvents  ? false : true;
      },
      submitEvents() {
          this.showEvents = false;
          this.$emit("onEventsUpdated", this.events)
      }
  }
};
</script>


<style scoped>
.pxEventHandler {
  float: left;
  width: auto;
  display: block;
}
label {
  float: left;
  padding-left: 15px;
  text-indent: -15px;
}
input {
  width: 15px;
  height: 15px;
  padding: 0;
  margin: 0;
  vertical-align: bottom;
  position: relative;
  top: -1px;
}
.fullForm {
  display: flex;
}
.openEventMenu {
    float: left;
}
modal {
  width: auto;
  height: auto;
  border: 1px solid #c3c3c3;
  display: flex;
  flex-wrap: wrap;
  align-content: center;
  margin: 5px;
}
</style>