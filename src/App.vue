<template>
  <Header />
  <Body />
</template>

<script>
import Header from "./components/header.vue";
import Body from './components/body.vue';

export default {
  name: "App",
  components: {
    Header,
    Body
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
  margin-top: 60px;
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
  border-color: #00FFFF;
  background-color: white;
}
</style>
