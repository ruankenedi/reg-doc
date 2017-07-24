
<template>
  <div style="width: 200px; max-width: 90vw; margin-left: 15px;">

    <q-input color="amber" v-model="terms" placeholder="Country-Code">
     <q-autocomplete v-if="selected" @click="inputCountry" @search="search" :min-characters="1" :static-data="{field: 'stamp', list: flags}"/>
</q-input>

  </div>
</template>

<script>
import {  QInput, QSelect, QIcon, QAutocomplete, QSearch, filter, QBtn, QField } from 'quasar'

export default {
  components: {
    QBtn,
    QAutocomplete,
    QSearch,
    QIcon,
    QInput,
    QField
  },
  // props:{
  //   countryCode: {
  //     type: Boolean,
  //     default: true,
  //     required: true
  //   }
  // },
  data () {
    return {
      countries: [
        {
          code: 376,
          shortName: 'AD',
          name: 'Andorra'
        },
        {
          code: 971,
          shortName: 'AE',
          name: 'Emirados Árabes Unidos'
        },
        {
          code: 93,
          shortName: 'AF',
          name: 'Afeganistão'
        },
        {
          code: 1,
          shortName: 'AG',
          name: 'Antígua e Barbuda'
        },
        {
          code: 1,
          shortName: 'AI',
          name: 'Anguilla'
        },
        {
          code: 355,
          shortName: 'AL',
          name: 'Albânia'
        },
        {
          code: 49,
          shortName: 'ALE',
          name: 'Alemanha'
        },
        {
          code: 374,
          shortName: 'AM',
          name: 'Armênia'
        },
        {
          code: 244,
          shortName: 'AO',
          name: 'Angola'
        },
        //não encontrado
          //code: ,
          //shortName: 'AQ',
          //name: ''
        //},
        {
          code: 54,
          shortName: 'AR',
          name: 'Argentina'
        },
        {
          code: 213,
          shortName: 'ARG',
          name: 'Argélia'
        },
        {
          code: 1,
          shortName: 'AS',
          name: 'Samoa Americana'
        },
        {
          code: 43,
          shortName: 'AT',
          name: 'Áustria'
        },
        {
          code: 61,
          shortName: 'AU',
          name: 'Austrália'
        },
        {
          code: 297,
          shortName: 'AW',
          name: 'Aruba'
        },
         //{não encontrado
          //code: 297,
          //shortName: 'AX',
          //name: ''
        //},
        {
          code: 994,
          shortName: 'AZ',
          name: 'Azerbaijão'
        },
        {
          code: 387,
          shortName: 'BA',
          name: 'Bósnia e Herzegovina'
        },
        {
          code: 1,
          shortName: 'BB',
          name: 'Barbados'
        },
        {
          code: 880,
          shortName: 'BD',
          name: 'Bangladesh'
        },
        {
          code: 32,
          shortName: 'BE',
          name: 'Bélgica'
        },
        //{
          //code: 297,
          //shortName: 'BF',
          //name: ''
        //},
        {
          code: 359,
          shortName: 'BG',
          name: 'Bulgária'
        },
        {
          code: 973,
          shortName: 'BH',
          name: 'Bahrein'
        },
        {
          code: 257,
          shortName: 'BI',
          name: 'Burundi'
        },
        {
          code: 229,
          shortName: 'BJ',
          name: 'Benin'
        },
        //{FRANÇA ESTRANHA
        //  code: 297,
         // shortName: 'BL',
         // name: ''
        //},
        {
          code: 1,
          shortName: 'BM',
          name: 'Bermudas'
        },
        {
          code: 673,
          shortName: 'BN',
          name: 'Brunei'
        },
        {
          code: 591,
          shortName: 'BO',
          name: 'Bolívia'
        },
        {
          code: 55,
          shortName: 'BR',
          name: 'Brasil'
        },
        {
          code: 1,
          shortName: 'BS',
          name: 'Bahamas'
        },
        {
          code: 975,
          shortName: 'BT',
          name: 'Butão'
        },
         //{mudar, shortName errado
          //code: 47,
         // shortName: 'BV',
        //  name: 'Noruega'
      //  },
        {
          code: 267,
          shortName: 'BW',
          name: 'Botsuana'
        },
        {
          code: 375,
          shortName: 'BY',
          name: 'Bielorrússia'
        },
        {
          code: 501,
          shortName: 'BZ',
          name: 'Belize'
        },
        {
          code: 1,
          shortName: 'CA',
          name: 'Canadá'
        },
        //{não econtrado
         // code: 297,
         // shortName: 'CC',
         // name: ''
        //},
        {
          code: 243,
          shortName: 'CD',
          name: 'Congo - Kinshasa'
        },
        {
          code: 242,
          shortName: 'CG',
          name: 'Congo - Brazzaville'
        },
        {
          code: 56,
          shortName: 'CH',
          name: 'Chile'
        },
        {
          code: 225,
          shortName: 'CI',
          name: 'Costa do Marfim'
        },
        {
          code: 682,
          shortName: 'CK',
          name: 'Ilhas Cook'
        },
        {
          code: 86,
          shortName: 'CN',
          name: 'China'
        },
        {
          code: 57,
          shortName: 'CO',
          name: 'Colômbia'
        },
        {
          code: 506,
          shortName: 'CR',
          name: 'Costa Rica'
        },
        {
          code: 53,
          shortName: 'CU',
          name: 'Cuba'
        },
        {
          code: 238,
          shortName: 'CV',
          name: 'Cabo Verde'
        },
        {
          code: 599,
          shortName: 'CW',
          name: 'Curaçao'
        },
        //{não encontrado
          //code: 236,
          //shortName: 'CX',
         // name: ''
        //},
        {
          code: 357,
          shortName: 'CY',
          name: 'Chipre'
        },
        {
          code: 420,
          shortName: 'CZ',
          name: 'Tchéquia'
        },
        {
          code: 45,
          shortName: 'DC',
          name: 'Dinamarca'
        },
        {
          code: 253,
          shortName: 'DJ',
          name: 'Djibuti'
        },
        {
          code: 1,
          shortName: 'DM',
          name: 'Dominica'
        },
        {
          code: 593,
          shortName: 'EQ',
          name: 'Equador'
        },

      //Daqui para baixo estão os countries certo, porém, não estão em ordem
        {
          code: 237,
          shortName: 'RC',
          name: 'República dos Camarões'
        },
        {
          code: 1,
          shortName: 'RD',
          name: 'República Dominicana'
        },
        {
          code: 236,
          shortName: 'RCF',
          name: 'República Centro-Africana'
        },
        {
          code: 297,
          shortName: 'SU',
          name: 'Suíça'
        },

        {
          code: 297,
          shortName: 'HL',
          name: 'Holanda'
        },
      ],
      terms: '',
      selected: true
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
       done(filter(terms, {field, list}))
    },
    inputCountry() {
      this.selected = false;
    },
  }
}
</script>

<style>
  img {
    width: 40px;
    height: 20px;
  }
</style>
