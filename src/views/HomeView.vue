<template>
  <div class="container" ref="scrollComponent">
    <div v-for="count in counts" :key="count" class="card">
      <DogCard />
    </div>
  </div>
</template>

<script>
import debounce from "lodash/debounce";
import DogCard from "../components/DogCard.vue";
export default {
  name: "home",
  components: { DogCard },
  data() {
    return {
      counts: 3,
    };
  },
  methods: {
    handleScroll(event) {
      this.isUserScrolling = window.scrollY > 0;
      this.counts += 3;
    },
  },
  mounted() {
    this.handleDebouncedScroll = debounce(this.handleScroll, 500);
    window.addEventListener("scroll", this.handleDebouncedScroll);
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.handleDebouncedScroll);
  },
};
</script>

<style scoped>
.container {
  min-height: 100vh;
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  margin: 1rem;
}
.card {
  flex-grow: 1;
  width: 30%;
  height: 40rem;
  border: 1px solid black;
  border-radius: 5%;
  background-color: gray;
}

@media only screen and (min-width: 10px) {
  .card {
    width: 100%;
  }
}
@media only screen and (min-width: 850px) {
  .card {
    width: 45%;
  }
}
@media only screen and (min-width: 1500px) {
  .card {
    width: 30%;
  }
}
</style>
