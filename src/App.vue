<template>
  <button @click="showAlert = true">Show Alert</button>
  <Alert
    msg="Data has been added with success"
    :show="showAlert"
    @hide="showAlert = false"
    type="warning"
    title="danger"
    position="bottom-right"
  />
</template>

<script>
import Alert from "./components/Alert";
export default {
  name: "App",
  data: () => ({
    showAlert: false,
  }),
  components: {
    Alert,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 20px;
}
</style>
