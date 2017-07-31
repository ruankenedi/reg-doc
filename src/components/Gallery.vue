<template>
  <div class="layout-padding row justify-center">
    <div>
      <q-input float-label="BUG" v-model="text" ref="inputinho" />
      <button @click="toggleDisplay()">vai</button>
    </div>
  </div>
</template>

<script>
import {
  QInput
} from 'quasar'
export default {
  components: {
    QInput
  },
  data () {
    return {
      text: ''
    }
  },
  methods:{

    toggleDisplay() {
      this.$refs.inputinho.focus();
    }
  }
}
</script>
