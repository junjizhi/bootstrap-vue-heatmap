<script>
import Vue from 'vue';
import BootstrapVueHeatmap from '@/bootstrap-vue-heatmap.vue';
import { BCard, BootstrapVueIcons} from 'bootstrap-vue'
Vue.component('b-card', BCard)
Vue.use(BootstrapVueIcons)

import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

const Cities = [
  'Berkeley',
  'Mexico City',
  'Mumbai',
  'New York',
  'Shanghai',
  'Tokyo',
  'Toronto'
];

export default Vue.extend({
  name: 'ServeDev',
  components: {
    BootstrapVueHeatmap
  },
  data() {
    return {
      nonNumericFields: ['City'],
      stickyFields: ['City'],
      numericFields: [
        '2021-06-27 8:00',
        '2021-06-27 8:10',
        '2021-06-27 8:20',
        '2021-06-27 8:30',
        '2021-06-27 8:40',
        '2021-06-27 8:50',
        '2021-06-27 9:00',
        '2021-06-28 8:00',
        '2021-06-28 8:10',
        '2021-06-28 8:20',
        '2021-06-28 8:30',
        '2021-06-28 8:40',
        '2021-06-28 8:50',
        '2021-06-28 9:00',
        '2021-06-29 8:00',
        '2021-06-29 8:10',
        '2021-06-29 8:20',
        '2021-06-29 8:30',
        '2021-06-29 8:40',
        '2021-06-29 8:50',
        '2021-06-30 9:00',
        '2021-06-30 8:00',
        '2021-06-30 8:10',
        '2021-06-30 8:20',
        '2021-06-30 8:30',
        '2021-06-30 8:40',
        '2021-06-30 8:50',
        '2021-06-30 9:00'
      ],
      data: Cities.map(city => ({
        City: city,
        '2021-06-27 8:00': Math.floor(Math.random() * 9),
        '2021-06-27 8:10': 1.234567,
        '2021-06-27 8:20': Math.floor(Math.random() * 9),
        '2021-06-27 8:30': Math.floor(Math.random() * 9),
        '2021-06-27 8:40': Math.floor(Math.random() * 9),
        '2021-06-27 8:50': Math.floor(Math.random() * 9),
        '2021-06-27 9:00': Math.floor(Math.random() * 9),
        '2021-06-28 8:00': Math.floor(Math.random() * 9),
        '2021-06-28 8:10': Math.floor(Math.random() * 9),
        '2021-06-28 8:20': Math.floor(Math.random() * 9),
        '2021-06-28 8:30': Math.floor(Math.random() * 9),
        '2021-06-28 8:40': Math.floor(Math.random() * 9),
        '2021-06-28 8:50': Math.floor(Math.random() * 9),
        '2021-06-28 9:00': Math.floor(Math.random() * 9),
        '2021-06-29 8:00': Math.floor(Math.random() * 9),
        '2021-06-29 8:10': Math.floor(Math.random() * 9),
        '2021-06-29 8:20': Math.floor(Math.random() * 9),
        '2021-06-29 8:30': Math.floor(Math.random() * 9),
        '2021-06-29 8:40': Math.floor(Math.random() * 9),
        '2021-06-29 8:50': Math.floor(Math.random() * 9),
        '2021-06-29 9:00': Math.floor(Math.random() * 9),
        '2021-06-30 8:00': Math.floor(Math.random() * 9),
        '2021-06-30 8:10': Math.floor(Math.random() * 9),
        '2021-06-30 8:20': Math.floor(Math.random() * 9),
        '2021-06-30 8:30': Math.floor(Math.random() * 9),
        '2021-06-30 8:40': Math.floor(Math.random() * 9),
        '2021-06-30 8:50': Math.floor(Math.random() * 9),
        '2021-06-30 9:00': Math.floor(Math.random() * 9)
      }))
    }
  }
});
</script>

<template>
  <div id="app">
    <b-card
      title="Heatmap"
    >
      <bootstrap-vue-heatmap
        :non-numeric-fields="nonNumericFields"
        :numeric-fields="numericFields"
        :sticky-fields="stickyFields"
        :data="data"
        :compact="false"
      />
    </b-card>
  </div>
</template>
