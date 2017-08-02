<template>
  <div class="layout-padding row justify-center">
    <RegDocuments @regDoc="method"></RegDocuments>
  </div>
</template>

<script>
import RegDocuments from './RegDocuments.vue'
import {
  Toast,
  QBtn,
  QModal,
  QModalLayout,
  QList,
  QItemMain
} from 'quasar'
export default {
  components: {
    QBtn,
    QModal,
    QModalLayout,
    QList,
    QItemMain,
    RegDocuments
  },
  data () {
    return {
      types: [
        {
          label: 'Visualizar',
          ref: 'maximizedModal'
        }
      ],
      position: 'bottom'
    }
  },
  methods: {
    openSpecialPosition (position) {
      this.position = position
      this.$nextTick(() => {
        this.$refs.positionModal.open()
      })
    },
    method(obj) {
      console.log(obj)
    }
  }
}
</script>
