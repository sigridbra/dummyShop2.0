<template>
  <TheNavBar />
  <TheBody />
</template>

<script>
import TheNavBar from "./components/TheNavBar.vue";
import TheBody from "./components/Thebody.vue";

export default {
  name: "App",
  components: {
    TheNavBar,
    TheBody,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {
   margin: 0 !important;
  }
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
button {
  border-radius: 200px;
  position: sticky;
  cursor: pointer;
}
input {
  border-color: #00ffff;
  background-color: white;
}
.flexbox {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: center;
  margin-top: 5px;
  gap: 10px;
}
</style>
