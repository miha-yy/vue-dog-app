<template>
  <div class="cards">
    <div v-if="!loading">
      <a :href="imageUrl" target="_blank">
        <img v-bind:src="imageUrl" />
      </a>
      <div class="breed">
        <h1>
          <a :href="link" target="_blank">
            {{ breed }}
          </a>
        </h1>
      </div>
    </div>
    <div class="waiting" v-else>
      <h1>Loading Image</h1>
    </div>
  </div>
</template>

<script>
export default {
  name: "DogCard",
  data() {
    return {
      image: "",
      breed: "",
      loading: true,
      link: "",
    };
  },
  methods: {
    async fetchData() {
      const res = await fetch("https://dog.ceo/api/breeds/image/random");
      const data = await res.json();
      return data;
    },
    async getData() {
      this.loading = true;
      const data = await this.fetchData();
      this.imageUrl = data.message;
      this.getBreed();
      this.link = "https://www.google.com/search?q=" + this.breed;
      this.loading = false;
    },
    getBreed() {
      let breeding = this.imageUrl.substring(
        this.imageUrl.indexOf("d") + 15,
        this.imageUrl.lastIndexOf("/")
      );
      let dash = breeding.replace("-", " ");
      this.breed = dash.charAt(0).toUpperCase() + dash.slice(1);
    },
  },
  async created() {
    const data = await this.fetchData();
    this.imageUrl = data.message;
    this.getBreed();
    this.link = "https://www.google.com/search?q=" + this.breed;
    this.loading = false;
  },
};
</script>

<style scoped>
.cards {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
}
.image {
  margin-top: 2rem;
}
img {
  border-radius: 1rem;
}
.breed {
  margin-top: 1.8rem;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  text-align: center;
  font-size: 1.5rem;
}
.breed a {
  color: rgb(66, 65, 65);
  font-weight: bolder;
  transition: opacity 0.5s;
  text-decoration: none;
}
.breed a:hover {
  opacity: 75%;
}
.waiting {
  margin-top: 15rem;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  text-align: center;
  font-size: 2rem;
}
@media only screen and (min-width: 10px) {
  .breed {
    font-size: 1.3rem;
  }
  img {
    width: 30rem;
    height: 30rem;
  }
}
@media only screen and (min-width: 850px) {
  .breed {
    font-size: 1.3rem;
  }
  img {
    width: 25rem;
    height: 30rem;
  }
}
@media only screen and (min-width: 1500px) {
  .breed {
    font-size: 1.5rem;
  }
  img {
    width: 35rem;
    height: 30rem;
  }
}
</style>
