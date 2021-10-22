<template>
  <div v-for="(value, key, index) in events" :key="index">
    <input type="checkbox" :id="key" v-model="events[key]" />
    <label :for="key">{{ key }}</label>
  </div>
  <button/>
</template>


<script>
export default {
  name: "pxEvents",
  data() {
    return {
      events: {
         "onPaymentCompleted": false ,
         "onPaymentPaid": false ,
         "onEventNotification": false ,
         "onInstrumentSelected": false ,
         "onExternalRedirect": false ,
         "onError": false ,
         "onTermsOfServiceRequested": false ,
         "onOutOfViewRedirect": false ,
         "OnApllicationConfigured": false ,
         "onPaymentAborted": false ,
         "onPaymentFailed": false ,
         "ExternalOpen": false ,
         "onOutOfViewOpen": false 
      },
    };
  },
};
</script>


<style scoped>
</style>