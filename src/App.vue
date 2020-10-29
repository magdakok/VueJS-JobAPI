<template>
  <Dashboard />
</template>

<script>
import Dashboard from "./components/Dashboard.vue";

export default {
  name: "App",
  components: {
    Dashboard,
  },
};
</script>

<style>
*,
*::after,
*::before {
  margin: 0;
  padding: 0;
  -webkit-box-sizing: inherit;
  box-sizing: inherit;
  font-family: inherit;
}

body {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}

ul {
  list-style: none;
}

body {
  font-family: "Spartan", sans-serif;
  font-size: 14px;
  color: #242b37;
}

.fade-enter {
  opacity: 0;
}
.fade-enter-to,
.fade-leave {
  opacity: 1;
}

.fade-enter-active {
  transition: opacity 0.4s;
}

.fade-leave-to {
  opacity: 0;
}

.fade-leave-active {
  transition: opacity 0.4s;
}
</style>
