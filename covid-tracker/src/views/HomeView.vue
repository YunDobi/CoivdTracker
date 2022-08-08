<template>
  <main v-if="!loading">
    Show data
  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="loadingImage" class="w-24 m-auto" alt="">
  </main>
</template>

<script>

export default {
  name: 'HomeView',
  components: {},
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      state: {},
      countries: [],
      loadingImage: require("../assets/logo.png")
    }
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch('https://api.covid19api.com/summary');
      const data = await res.json();
      return data;
    }
  },
  async created() {
    const data = await this.fetchCovidData()
  

    this.dataDate = data.Date;
    this.state = data.Global;
    this.countries = data.Countries;
    this.loading = false;

  },
}
</script>
