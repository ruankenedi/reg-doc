<template>
  <div class="layout-padding row justify-center">
    <div style="width: 500px; max-width: 90vw;">
      <div>
        <q-btn color="primary" >
          <q-icon name="assignment" />
          <q-popover ref="popover1">
            <q-list link separator class="scroll" style="min-width: 150px" >

                <q-btn v-if="selected" @click="inputCountry">
                <img src="../assets/flags/4x3/br.svg" v-if="selected" @click="inputCountry">
                <aside style="margin-left: 20px;">Brasil</aside>
                  <sub style="margin-left: 20px; margin-top: 2px;">+55</sub>
                  </q-btn>
                  <q-field v-else>
                    <q-input></q-input>
                  </q-field>
            </q-list>
          </q-popover>
        </q-btn>
      </div>
    </div>
  </div>
</template>

<script>
import {
  Toast,
  QBtn,
  QPopover,
  QList,
  QItem,
  QItemMain,
  QIcon,
  QRadio,
  QCard,
  QCardTitle,
  QCardMain,
  QChip,
  QFixedPosition,
  QInput,
  QField
} from 'quasar'
export default {
  components: {
    QInput,
    QBtn,
    QPopover,
    QList,
    QItem,
    QItemMain,
    QIcon,
    QRadio,
    QCard,
    QCardTitle,
    QCardMain,
    QChip,
    QFixedPosition,
    QField
  },
  data () {
    return {
      anchorOrigin: {vertical: 'bottom', horizontal: 'left'},
      selfOrigin: {vertical: 'top', horizontal: 'left'},
      selected: true
    }
  },
  methods: {
    inputCountry() {
      this.selected = true;
    }
  },
  computed: {
    anchor () {
      return `${this.anchorOrigin.vertical} ${this.anchorOrigin.horizontal}`
    },
    self () {
      return `${this.selfOrigin.vertical} ${this.selfOrigin.horizontal}`
    }
  }
}
</script>

<style>
  img {
    width: 15px;
    height: 15px;
  }
</style>
