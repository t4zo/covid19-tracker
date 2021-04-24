<template>
  <div class="text-center">
    <h2 class="text-4xl font-bold uppercase">{{ text }}</h2>
    <div class="text2-xl mt-4 mb-10">
      {{ timestamp }}
    </div>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, reactive } from 'vue';
import moment from 'moment';

export default defineComponent({
  name: 'Title',
  props: {
    text: String,
    date: Date,
  },
  // Vue 3
  setup({ text, date }) {
    const state = reactive({
      timestamp: computed(() => {
        return moment(date).locale('pt-br').format('LLLL');
      })
  });

    return state;
  },
  // Vue 2
  // computed: {
  //   timestamp: ({ date }: any) => {
  //     return moment(date).locale('pt-br').format('LLLL')
  //   }
  // },
})
</script>