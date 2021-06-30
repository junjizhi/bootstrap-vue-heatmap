<script>
import Vue from 'vue'
import { BTable } from 'bootstrap-vue'

Vue.component('b-table', BTable)

export default /*#__PURE__*/{
  name: "BootstrapVueHeatmap",
  props: {
    /**
     * A list of non-numeric fields (strings). These columns will not be color-coded.
    */
    nonNumericFields: Array,
    /**
     * A list of numeric fields (strings). These columns will be color-coded.
    */
    numericFields: Array,
    /**
     * A list of data objects. The keys of each object should be either a numeric or non-numeric field.
    */
    data: Array,
  },
  computed: {
    fields: function() {
      return [
        ...this.nonNumericFields.map(c => ({key: c, label: c, sortable: true})),
        ...this.numericFields.map(c => ({key: c, label: c, sortable: true})),
      ]
    },
    items: function() {
      return this.addCellVariants(this.data)
    }
  },
  methods: {
    addCellVariants(data) {
      const HEAT_MAX = 8

      const allValues = data.map(item => {
        return this.numericFields.map(c => item[c])
      }).flat()

      const globalMax = Math.max(...allValues);
      const globalMin = Math.min(...allValues);
      const scale = globalMax - globalMin;

      return data.map(item => {
        const variants = {};
        this.numericFields.forEach(c => {
          const value = item[c]
          const offset = value - globalMin;
          const heat = Math.floor((offset / scale) * HEAT_MAX)
          variants[c] = 'heat-' + heat
        })

        return {
          ...item,
          _cellVariants: variants
        }
      })
    }
  }
}
</script>

<template>
  <div class="heatmap-wrapper">
    <b-table
      small
      bordered
      sticky-header="58vh"
      head-variant="light"
      responsive
      :fields="fields"
      :items="items"
    />
  </div>
</template>

<style scoped>
/* https://colorbrewer2.org/#type=sequential&scheme=Oranges&n=9 */
.heatmap-wrapper {
  --heat-0: #fff5eb;
  --heat-1: #fee6ce;
  --heat-2: #fdd0a2;
  --heat-3: #fdae6b;
  --heat-4: #fd8d3c;
  --heat-5: #f16913;
  --heat-6: #d94801;
  --heat-7: #a63603;
  --heat-8: #7f2704;
}
</style>

<style>

.table-heat-0 {
  background-color: var(--heat-0);
}

.table-heat-1 {
  background-color: var(--heat-1);
}

.table-heat-2 {
  background-color: var(--heat-2);
}

.table-heat-3 {
  background-color: var(--heat-3);
}

.table-heat-4 {
  background-color: var(--heat-4);
}

.table-heat-5 {
  background-color: var(--heat-5);
}

.table-heat-6 {
  background-color: var(--heat-6);
}

.table-heat-7 {
  background-color: var(--heat-7);
}

.table-heat-8 {
  background-color: var(--heat-8);
}
</style>