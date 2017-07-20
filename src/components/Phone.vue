<template>
  <div class="layout-padding row justify-center">
      <q-input id="phone" float-label="Phone" style="width: 215px;"/>
    <div style="width: 215px; max-width: 90vw; margin-left: 15px;">
       <q-input id="label" color="amber" v-model="terms" float-label="Label">
          <q-autocomplete @search="search" :min-characters="1" @selected="selected" :static-data="{field, list}"/>
       </q-input>
    </div>
  </div>
</template>

<script>

// function startLabel() {
//   if() {

//   }
// }

import {
  QAutocomplete,
  QSearch,
  QInput,
  uid,
  filter,
  Toast,
  QSelect,
  QIcon
} from 'quasar'

export default {
  components: {
    QAutocomplete,
    QSearch,
    QInput,
    QSelect,
    QIcon
  },
  data () {
    return {
      terms: '',
      field: 'value',
        list: [
          {
            value: 'Residential', // The value given, when selected
            label: 'Residential', // The value displayed as main label for this suggested selection
          },
          {
            value: 'Commercial', // The value given, when selected
            label: 'Commercial', // The value displayed as main label for this suggested selection
          },
          {
            value: 'Cell Phone', // The value given, when selected
            label: 'Cell Phone', // The value displayed as main label for this suggested selection
          },
          {
            value: 'Other', // The value given, when selected
            label: 'Other', // The value displayed as main label for this suggested selection
          }
        ],
    }
  },
  methods: {
    search (terms, done) {
      setTimeout(() => {
        done(filter(terms, {field, list}))
      }, 100)
    },
  }
}
</script>
