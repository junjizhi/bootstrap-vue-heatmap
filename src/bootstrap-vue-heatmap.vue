<script>
import Vue from 'vue'
import { BTable } from 'bootstrap-vue'
import { BTooltip, BootstrapVueIcons} from 'bootstrap-vue'

Vue.component('b-table', BTable)
Vue.component('b-tooltip', BTooltip)
Vue.use(BootstrapVueIcons)

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
    /**
     * A flag to indicate if the heatmap is rendering in compact mode. It allows the heatmap to show more data with less horizontal span.
    */
    compact: Boolean,
    /**
     * A list of fields that are stick to the left of the heatmap when the heatmap has a horizontal scrollbar.
    */
    stickyFields: {
      type: Array,
      default: () => [],
    },
    /**
     * Formats a the numermic cells using Javascript fixed-point notation. If passed in as a number, it denotes the number of decimal places to display. Defaults to 2 decimal places
    */
    fixedDecimalPlaces: {
      type: [Number, Boolean],
      default: () => 2,
    },
  },
  computed: {
    fields: function() {
      return [
        ...this.columnConfigs(this.nonNumericFields, this.stickyFields),
        ...this.columnConfigs(this.numericFields, this.stickyFields)
      ]
    },
    items: function() {
      return this.addCellVariants(this.data)
    }
  },
  methods: {
    columnConfigs (fields, stickyFields) {
      return fields.map(function (c) { return { key: c, label: c, sortable: true, stickyColumn: stickyFields.includes(c) } })
    },
    addCellVariants(data) {
      const HEAT_MAX = 8

      const allValues = data.map(item => {
        return this.numericFields.map(c => item[c])
      }).flat().filter(n => !isNaN(n))

      let globalMin = 0
      let globalMax = 0
      let scale = 0

      if (allValues.length > 0) {
        globalMax = Math.max(...allValues);
        globalMin = Math.min(...allValues);
        scale = globalMax - globalMin;
      }

      return data.map(item => {
        const variants = {};
        this.numericFields.forEach(c => {
          const value = item[c]
          if(!isNaN(value) && scale != 0) {
            const offset = value - globalMin;
            const heat = Math.floor((offset / scale) * HEAT_MAX)
            variants[c] = 'heat-' + heat
          }
        })

        return {
          ...item,
          _cellVariants: variants
        }
      })
    },
    formatCellValue(item) {
      if (typeof this.fixedDecimalPlaces === 'boolean') {
        if (this.fixedDecimalPlaces) {
          return this.maybeFormat(item.value, 2)
        } else {
          return item.value
        }
      }
      if (Number.isInteger(this.fixedDecimalPlaces)) {
        return this.maybeFormat(item.value, this.fixedDecimalPlaces)
      }
      return item.value
    },
    maybeFormat(value, n) {
      try {
        return value.toFixed(n)
      } catch(Exception) {
        return value
      }
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
    >
      <template #head()="headData">
        <span v-if="nonNumericFields.includes(headData.label) || !compact">{{ headData.label }}</span>
        <b-icon
          v-if="!nonNumericFields.includes(headData.label) && !!compact"
          icon="clock"
          :title="headData.label"
        />
      </template>

      <template #cell()="cellData">
        <span v-if="nonNumericFields.includes(cellData.field.key) || !compact">{{ formatCellValue(cellData) }}</span>
        <div
          v-if="numericFields.includes(cellData.field.key) && compact"
          :title="cellData.value"
        >
&nbsp;
        </div>
      </template>
    </b-table>
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