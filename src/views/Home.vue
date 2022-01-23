<template>
  <main v-if="!loading">
    <Title :text="title" :date="date" />
    <Boxes :stats="stats" />
    <div class="flex my-10">
      <CountrySelect :countries="countries" @changeCountryStats='changeCountryStats' />
      <button v-if="stats.Country" class="bg-green-700 text-white rounded p-3 block focus:outline-none hover:bg-green-600" @click="clearCountrySelect">
        Limpar pais
      </button>
    </div>
  </main>
  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Buscando dados
    </div>
    <img :src="loadingImage" alt="" class="w-24 m-auto">
  </main>
</template>

<script>
import { defineComponent, ref, reactive, onMounted } from "vue";
import axios from "axios";

import Title from '@/components/Title';
import Boxes from '@/components/Boxes';
import CountrySelect from '@/components/CountrySelect';

export default defineComponent({
  name: "Home",
  components: {
    Title,
    Boxes,
    CountrySelect,
  },
  async setup() {
    const state = reactive({
      loading: true,
      title: 'Global',
      stats: {},
      countries: [],
      date: Date,
      loadingImage: require('../assets/loading.gif')
    });

    // onMounted(async () => {
      await setInitialState();
      state.loading = false;
    // });

    function changeCountryStats(country) {
      console.log(state)
      state.stats = country;
      state.title = country.Country;
      console.log(state)
    };

    function clearCountrySelect() {
      state.value.title = 'Global';
      setInitialState();
    };

    async function fetchCovidData() {
      try {
      const response = await axios.get("https://api.covid19api.com/summary");
      return response.data;
      } catch(error) {
        console.error(error);
      }
    };

    async function setInitialState() {
      state.loading = true;
      const data = await fetchCovidData();
      state.stats = data.Global;
      state.date = new Date(data.Date);
      state.countries = data.Countries;
      state.loading = false;
    };

    const response = {
      ...state,
      changeCountryStats,
      clearCountrySelect,
    };

    return response;
  }});
// data() {
//   return {
//     loading: true,
//     title: 'Global',
//     stats: {},
//     countries: [],
//     date: Date,
//     loadingImage: require('../assets/loading.gif')
//   };
// },
// async created() {
//   await this.setInitialState();
//   this.loading = false;
// },
//   methods: {
//     async fetchCovidData() {
//       try {
//       const response = await axios.get("https://api.covid19api.com/summary");
//       return response.data;
//       } catch(error) {
//         console.error(error);
//       }
//     },
//     changeCountryStats(country) {
//       this.stats = country;
//       this.title = country.Country
//     },
//     clearCountrySelect() {
//       this.title = 'Global';
//       this.setInitialState();
//     },
//     async setInitialState() {
//       this.loading = true;
//       const data = await this.fetchCovidData();
//       this.stats = data.Global;
//       this.date = new Date(data.Date);
//       this.countries = data.Countries;
//       this.loading = false;
//     },
//   },
// });
</script>
