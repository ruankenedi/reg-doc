<template>
  <div style="width: 215px; max-width: 90vw; margin-left: 15px;">
    <q-input id="label" color="amber" v-model="terms" float-label="Label">
      <q-autocomplete @search="search" :min-characters="1" @selected="selected" :static-data="{field: 'value', list: flags}"/>
    </q-input>
  </div>
</template>

<script>
import {  QInput, QSelect, QIcon, QAutocomplete, QSearch } from 'quasar'

export default {
  components: {
    QAutocomplete,
    QSearch,
    QIcon,
    QInput
  },
  props:{

  },
  data () {
    return {
      countries: [
        {
          code: 55,
          shortName: 'BR',
          name: 'Brasil'
        },
        {
          code: 376,
          shortName: 'AD',
          name: 'Andorra'
        }
      ],

      selected: '',
      terms: ''
    }
  },
  computed: {
    flags() {
      return this.countries.map((country) => {
        return {
          avatar: require(`../assets/flags/4x3/${country.shortName.toLowerCase()}.svg`),
          label: country.name,
          value: country.shortName,
          stamp: `+${country.code}`
        };
      })
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

 <style>

 </style>


