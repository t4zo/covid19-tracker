<template>
  <select name="country" id="country" v-model="selected" class="form-select block flex-grow border p-3 rounded focus:outline-none" @change="changeCountryStats">
    <option value="0">Select Country</option>
    <option v-for="c in countries" :value="c.ID" :key="c.ID">
      {{ c.Country }}
    </option>
  </select>
</template>

<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'CountrySelect',
  props: {
    countries: {}
  },
  // Vue 2
  // data() {
  //   return {
  //     selected: 0,
  //   }
  // },
  // Vue 3
  emits: ['changeCountryStats'],
  setup({ countries }, { emit }) {
    const selected = ref(0);
    const changeCountryStats = (e) => {
      const countryId = e.target.value;
      const country = countries.find(c => c.ID == countryId);
      emit('changeCountryStats', country);
    }

    return {
      selected,
      changeCountryStats,
    };
  }
  // Vue 2
  // methods: {
  //   changeCountryStats(e) {
  //     const countryId = e.target.value;
  //     const country = this.countries.find(c => c.ID == countryId);
  //     this.$emit('changeCountryStats', country);
  //   }
  // },
})
</script>
