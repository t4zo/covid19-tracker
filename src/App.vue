<template>
  <Header />
  <div class="container">
    <router-view />
  </div>
</template>

<script lang="ts">
// @ is an alias to /src
import { defineComponent } from 'vue';
import Header from "@/components/Header.vue";

export default defineComponent({
  components: {
    Header
  }
})
</script>

// <style scoped lang="scss">
//   .container {
//     width: 60%;
//     margin: auto;
//   }
// </style>
