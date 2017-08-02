<template>
  <div class="layout-padding row justify-center">
    <div style="display: flex;">
      <q-field style="width: 115px;">
        <q-select v-if="!showInput" v-model="select" :options="selectOptions" @change="toggleDisplay" float-label="Document"/>

        <q-input v-show="showInput" ref="input1" @blur="blur" v-model="text" float-label="Other document"/>
      </q-field>
      <q-field style="width: 135px;">
        <q-input v-model="inputValue" @blur="emitData" float-label="Document Number"/>
      </q-field>
      <div>
        <q-btn icon="photo library" color="primary"  style="margin-top: 22px; margin-left: 5px;"
        link v-for="modal in types" :key="modal" @click="requestFullscreen, modalFull" v-ripple.mat>
        view
            <!-- <q-item-main :label="modal.label" @click="modalFull"/>   <q-icon name="photo library" style="margin: 2px;"></q-icon>view -->
        </q-btn>
      </div>
        <q-modal ref="maximizedModal" maximized :content-css="{padding: '0px'}">
          <div :style="{display: none}">
            <q-gallery-carousel ref="gallery" fullscreen infinite dots :src="gallery"></q-gallery-carousel>
          </div>
        </q-modal>
    </div>
  </div>

</template>

<script>
import QGalleryCarousel from './Comp.vue'
import { QField, QSelect, QBtn, QInput, QModal, QModalLayout, QList, QItemMain, Ripple, QGallery, QIcon } from 'quasar'

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
    QGalleryCarousel,
    QIcon,
    QField
  },
  props: {
    // documentType: {
    //   type: String,
    //   required: true
    // },
    // numberDoc: {
    //   type: Number,
    //   required: true
    // },
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
      none: 'none',
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
          ref: 'maximizedModal'
        }
        // {
        //   label: 'Foto',
        //   ref: ''
        // },
        // {
        //   label: 'Update Imagem',
        //   ref: ''
        // }
      ],
      numberDocuments : [
        {
          label: 'CPF',
          number: '123'
        }
      ],
      gallery: [
         require('src/assets/vue.png'),
         require('src/assets/js.png'),
         require('src/assets/react.png'),
         require('src/assets/npm.png'),
         require('src/assets/node.png'),
         require('src/assets/quasar-logo-full.svg')
      ],
      showInput: false,
      inputValue: '',
      position: 'bottom'
    }
  },
  updated() {
    if (this.select === 'Other') {
      this.$refs.input1.focus();
    }
  },
  methods: {
    toggleDisplay(selected) {
      if (selected === 'Other') {
        this.showInput = true;
        return;
      }
      this.showInput = false;
    },
    requestFullscreen() {
       if (this.$refs.gallery) {
        this.$refs.gallery.$refs.slider.toggleFullscreen();
      }
    },
    modalFull() {
      this.none = 'flex';
    },
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
    emitData() {
      console.log(this.$emit('regDoc', {
      doc: this.select,
      num: this.inputValue
    }))
    }
  }
}
</script>

<style>

</style>
