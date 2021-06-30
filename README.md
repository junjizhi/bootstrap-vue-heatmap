# bootstrap-vue-heatmap

## Introduction
A simple heatmap component based on [Bootstrap-Vue](https://bootstrap-vue.org/) tables (a.k.a, `b-table`)

## Screenshots
![image](https://user-images.githubusercontent.com/2715151/123905669-c3bcd980-d940-11eb-9a1b-b9ac45d22282.png)
## Dependencies


* [Vue.js 2.6+](https://vuejs.org/2016/04/27/announcing-2.0/)
* [Bootstrap-Vue (v2.21.2+)](https://bootstrap-vue.org/)
* [Other Bootstrap-Vue dependencies](https://bootstrap-vue.org/docs).

## Installation

```bash
npm i bootstrap-vue-heatmap

# if you use yarn:

yarn add bootstrap-vue-heatmap
```

## Usage

```html
<script>
import Vue from 'vue';
import BootstrapVueHeatmap from '@/bootstrap-vue-heatmap.vue';
import { BCard } from 'bootstrap-vue'
Vue.component('b-card', BCard)

// Uncomment the following to import BootstrapVue CSS files if you
// have not done so when registering BootstrapVue. Order is important.
// Check out: https://bootstrap-vue.org/docs#using-module-bundlers
// import 'bootstrap/dist/css/bootstrap.min.css'
// import 'bootstrap-vue/dist/bootstrap-vue.css'

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
      numericFields: [
        '2021-06-27 8:00',
        '2021-06-27 8:10',
        '2021-06-27 8:20',
        '2021-06-27 8:30',
        '2021-06-27 8:40',
        '2021-06-27 8:50',
        '2021-06-27 9:00'
      ],
      data: Cities.map(city => ({
        City: city,
        '2021-06-27 8:00': Math.floor(Math.random() * 9),
        '2021-06-27 8:10': Math.floor(Math.random() * 9),
        '2021-06-27 8:20': Math.floor(Math.random() * 9),
        '2021-06-27 8:30': Math.floor(Math.random() * 9),
        '2021-06-27 8:40': Math.floor(Math.random() * 9),
        '2021-06-27 8:50': Math.floor(Math.random() * 9),
        '2021-06-27 9:00': Math.floor(Math.random() * 9)
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
        :data="data"
      />
    </b-card>
  </div>
</template>

```


## Features
- [ ] Support custom color pallette
- [ ] Support custom cell rendering as slots

## Component Reference
### Props

| Name                 | Type    | Description                                                                                                     |
| -------------------- | ------- | --------------------------------------------------------------------------------------------------------------- |
| `non-numeric-fields` | `Array` | A list of non-numeric fields (strings). These columns will not be color-coded.                                  |
| `numeric-fields`     | `Array` | A list of numeric fields (strings). These columns will be color-coded.                                          |
| `data`               | `Array` | A list of data objects. The keys of each object should be either a numeric or non-numeric field. Order matters. |

## Development

**Install dependencies**:
```bash
yarn install --dev
```

**Build component**:
```bash
yarn build
```

**Run example app locally**:
```bash
yarn serve
```

**Lints and fixes files**:
```bash
yarn lint
```

**Generate component documentation**:
```bash
yarn doc src/bootstrap-vue-heatmap.vue
```

## License

Released under the MIT [License](./LICENSE). Copyright (c) Bootstrap-vue-heatmap.