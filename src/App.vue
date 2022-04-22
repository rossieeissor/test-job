<template>
  <div class="container">
    <div v-if="isError" class="error">Something went wrong ...</div>
    <div v-else class="app">
      <user-profile :profile="profile" :profileIsLoading="profileIsLoading" />
      <div v-if="!profileIsLoading" class="beer-section">
        <beer-info :beerIsLoading="beerIsLoading" :beerInfo="beerInfo" />
        <button @click="changeBeer()" class="beer-changer">
          Choose Another Beer
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import userProfile from "@/components/UserProfile.vue";
import BeerInfo from "@/components/BeerInfo.vue";

export default {
  components: { userProfile, BeerInfo },

  data() {
    return {
      profile: {
        avatar: "",
        first_name: "",
        date_of_birth: "",
        employment: { title: "" },
      },

      profileIsLoading: false,

      beerInfo: {
        name: "",
        brand: "",
        style: "",
        hop: "",
      },

      beerIsLoading: false,

      isError: false,
    };
  },
  methods: {
    async fetchBeer() {
      this.beerIsLoading = true;
      try {
        const response = await fetch(
          "https://random-data-api.com/api/beer/random_beer"
        );
        const data = await response.json();
        this.beerInfo = data;
      } catch (error) {
        this.isError = true;
      }
      this.beerIsLoading = false;
    },

    async fetchData() {
      this.isError = false;
      this.profileIsLoading = true;

      try {
        const response = await fetch(
          "https://random-data-api.com/api/users/random_user"
        );
        const data = await response.json();
        this.profile = data;
      } catch (error) {
        this.isError = true;
      }
      this.profileIsLoading = false;
      this.fetchBeer();
    },

    async changeBeer() {
      this.fetchBeer();
    },
  },
  mounted() {
    this.fetchData();
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Kumbh Sans", sans-serif;
}

.container {
  background: #e3b448;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.app {
  background: #cbd18f;
  width: 80%;
  min-height: 500px;
  display: grid;
  grid-template-columns: auto;
  grid-template-rows: 220px 250px;
  gap: 20px;
  margin: 0 auto;
  padding: 30px;
}

.beer-section {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
}

.beer-changer {
  padding: 5px;
}

.beer-changer {
  width: 180px;
  border: none;
  border-radius: 6px;
  background-color: #3a6b35;
  color: #e3b448;
  font-size: 1.2rem;
  font-family: "Karla", sans-serif;
  cursor: pointer;
  padding: 10px 20px;
}

.beer-changer:focus {
  outline: none;
}

.beer-changer:active {
  box-shadow: inset 5px 5px 10px -3px rgba(0, 0, 0, 0.7);
}

@media screen and (max-width: 768px) {
  .app {
    width: 100%;
    min-height: 500px;
    grid-template-columns: auto;
    grid-template-rows: minmax(40vh, 1fr) minmax(45vh, 1.13fr);
    gap: 20px;
    margin: 0 auto;
    padding: 30px;
  }
}
</style>
