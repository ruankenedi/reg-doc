<template>
  <div>
    <s-doc-field v-model="myDoc"></s-doc-field >

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

      myDoc: {
        value: '',
        label: '',
        number: '',
        gallery: [
          require('src/assets/js.png')
        ]
      }
    }
  }
}
</script>





