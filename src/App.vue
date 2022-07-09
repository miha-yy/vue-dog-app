<script>
import { RouterView } from "vue-router";
import NavBar from "./components/NavBar.vue";
export default {
  components: { NavBar },
  data() {
    return {};
  },
};
</script>

<template>
  <NavBar />
  <RouterView />
</template>
