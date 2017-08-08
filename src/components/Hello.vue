<template>
  <div>
    <s-doc-field v-model="myDoc" ></s-doc-field >
  </div>
</template>

<script>
import sDocField from './RegDocuments.vue';

export default {
  name: 'index',
  components: {
    sDocField
  },
  data() {
    return {
      myTypes: [
        'CPF',
        'RG',
        'CERTIDÃO DE NASCIMENTO'
      ],
      //myDoc: {}

      myDoc: {
        value: '',
        label: '',
        number: '',
        pictures: [

        ]
      },

      // docTypes: [
      //   {
      //     label: 'CPF',
      //     value: 'cpf'
      //   },
      //   {
      //     label: 'Certidão de Nascimento',
      //     value: 'birthReg'
      //   }
      // ]
    }
  },
  methods: {
    get(obj) {
      return this.myDoc = obj;
    }
  }
}
</script>





