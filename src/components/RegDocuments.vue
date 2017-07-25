<template>
  <div style="width: 215px; max-width: 90vw; margin-left: 15px;">
    <div>
    <q-select v-if="showSelect" v-model="select" :options="selectOptions" float-label="Document"/>
    <q-input v-if="showInput" @blur="blur" autofocus v-model="text" float-label="Other document"/>
    <q-input v-if="input" v-model="inputValue" float-label="Number of Document"/>
    </div>
       {{ show }}
    <div style="width: 103px; display: flex;">
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
            </q-btn>
        </q-modal-layout>
     </q-modal>

    <q-modal ref="maximizedModal" maximized :content-css="{padding: '50px'}">
      <h4></h4><p>Images</p>
       <div class="layout-padding row justify-center">
        <div style="width: 500px; max-width: 90vw;">
          <p class="caption">Oferecimento:</p>
          <q-gallery :src="gallery"></q-gallery>
        </div>
       </div>
      <q-btn style="margin-left: 95%;" color="tertiary" @click="$refs.maximizedModal.close()">Close</q-btn>
    </q-modal>

  </div>

</template>

<script>
import { QSelect, QBtn, QInput, QModal, QModalLayout, QList, QItemMain, Ripple, QGallery, QGalleryCarousel } from 'quasar'

export default {
  name: 'RegDocuments',
  components: {
    QSelect,
    QBtn,
    QInput,
    QModal,
    QModalLayout,
    QList,
    Ripple,
    QItemMain,
    QGallery,
    QGalleryCarousel
  },
  props: {
    documentType: {
      type: String,
      required: true
    },
    value: {
      type: Number,
      required: true
    },
    images: {
      type: Array,
      required: false
    }
  },
  directives: {
    Ripple
  },
  data () {
    return {
      text: '',
      select: '',
      selectOptions: [
        {
          label: 'RG',
          value: 'RG'
        },
        {
          label: 'CPF',
          value: 'CPF'
        },
        {
          label: 'Other',
          value: 'Other'
        }
      ],
      types: [
        {
          label: 'Visualizar',
          ref: 'maximizedModal'
        },
        {
          label: 'Upload de Imagens',
          ref: ''
        },
        {
          label: 'Tirar Fotos',
          ref: ''
        }
      ],
      gallery: [
         require('src/assets/vue.png'),
         require('src/assets/js.png',),
         require('src/assets/react.png',),
         require('src/assets/npm.png',),
         require('src/assets/node.png',),
         require('src/assets/quasar-logo-full.svg')
      ],
      showInput: false,
      showSelect: true,
      input: true,
      inputValue: '',
      position: 'bottom'
    }
  }, // event change
  methods: {
    blur() {
      const text = this.text
      if (text === text) {
        this.showInput = false;
        this.showSelect = true;
        this.input = true;
        this.select = '';
        this.selectOptions.push({
          label: text,
          value: text
        });
      }
    },
    openSpecialPosition (position) {
      this.position = position;
      this.$nextTick(() => {
      this.$refs.positionModal.open();
      });
    }
  },
  computed: {
    show() {
      if (this.select === 'Other') {
        this.showInput = true;
        this.showSelect = false;
        this.input = false;
      }
    }
  }
}
</script>

<style>

</style>
