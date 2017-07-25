<template>
  <div class="layout-padding row justify-center">
    <div style="width: 103px; max-width: 90vw;">
        <q-btn
          link
          v-for="modal in types"
          :key="modal"
          @click="$refs[modal.ref].open()"
          v-ripple.mat
        >
          <q-item-main :label="modal.label" />
        </q-btn>
    </div>
   <q-modal ref="layoutModal" :content-css="{minWidth: '80vw', minHeight: '80vh'}">
        <q-modal-layout>
            <q-btn flat @click="$refs.layoutModal.close()">
                <q-icon name="keyboard_arrow_left" />
            </q-btn>
        </q-modal-layout>
     </q-modal>

    <q-modal ref="maximizedModal" maximized :content-css="{padding: '50px'}">
      <h4>Maximized Modal</h4><p>This one is maximized on bigger screens too.</p>
      <q-btn color="tertiary" @click="$refs.maximizedModal.close()">Close Me</q-btn>
    </q-modal>


  </div>
</template>

<script>
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
    QItemMain
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
    }
  }
}
</script>
