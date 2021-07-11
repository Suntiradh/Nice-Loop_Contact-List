<template>
  <div id="nav">
    <h3>Contact List</h3>
    <br>
    <ContactList/>
  </div>
</template>
<script>
import ContactList from './components/ContactList.vue'

export default {
  name: "App",
  components: {
    ContactList,
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
  width: 60%;
  margin: 20px auto;
}
</style>
