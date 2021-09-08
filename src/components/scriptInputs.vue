<template>
  <div id="scriptOptions">
    <div class="inputs">
      <input
        class="input"
        id="link"
        placeholder="your link"
        v-model="link"
        @input="setInstrument"
      />
      <button v-on:click="clickOpen" class="submit" id="submitButton">
        open script
      </button>
    </div>
    <checkoutOptions
      :instrument="instrument"
      :settings="settings"
      @onUpdateSettings="settings = $event"
    />
  </div>
</template>

<script>
import checkoutOptions from "./checkoutOptions.vue";

export default {
  name: "scriptInputs",
  props: ["instrument"],
  watch: {
    settings: function (newVal) {
      this.$emit("onSettingsUpdated", newVal);
    },
  },
  components: {
    checkoutOptions,
  },
  data() {
    return {
      settings: "",
    };
  },
  methods: {
    async clickOpen() {
      this.injectScript(this.link)
        .then(() => {
          this.$emit("onScriptAppend");
        })
        .catch((error) => {
          window.alert("injection failed: " + error);
        });
    },
    async injectScript(src) {
      return new Promise((resolve, reject) => {
        // TODO: destroy previous script.
        const script = document.createElement("script");
        script.async = false;
        script.src = src;
        script.addEventListener("load", resolve);
        script.addEventListener("error", () => reject("Error loading script."));
        script.addEventListener("abort", () =>
          reject("Script loading aborted.")
        );
        document.head.appendChild(script);
      });
    },
    setInstrument(event) {
      const newValue = event.target.value;
      if (newValue.includes("payex")) {
        const splitValues = newValue.split("/");
        let instrumentName = splitValues[3];
        if (instrumentName.includes("creditcard"))
          instrumentName = "creditCard";
        else if (instrumentName.includes("paymentmenu"))
          instrumentName = "paymentMenu";
        this.$emit("onUpdateInstrument", instrumentName);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.inputs {
  position: left;
  width: auto;
  display: block;
}
.input {
  float: left;
  width: 70%;
}
.submit {
  display: inline-block;
}
</style>
