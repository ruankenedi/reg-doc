<template>
<div class="layout-padding row justify-center">
  <div style="display: flex;">
    <div style="width: 180px; margin-left: -200px;">
    <q-select v-if="!showInput" v-model="select" :options="selectOptions" @change="toggleDisplay" float-label="Document"/>
    </div>
    <div style="width: 180px; margin-left: -200px;">
    <q-input v-show="showInput" ref="input1" @blur="blur" v-model="text" float-label="Other document"/>
    </div>
    <div style="margin-left: 30px;">
    <q-input v-model="inputValue" float-label="Number of Document"/>
    </div>
    <div style="width: 400px; display: flex; margin-left: 10px;">
        <q-btn
          class="flex inline shadow-box flex-center"
          standard style="width: 200px; height: 10px; margin-top: 20px; background-color: dark; background-color: #dddddd;"
          link
          v-for="modal in types"
          :key="modal"
          @click="$refs[modal.ref].open()"
          v-ripple.mat
        >
          <q-item-main :label="modal.label" @click="modalFull"/>
        </q-btn>
    </div>

    <q-modal ref="maximizedModal" maximized :content-css="{padding: '0px', height: '567px', width: '100%'}" >
<div :style="{display: none}">
        <q-gallery-carousel style="height: 567px; width: 100%;" infinite autoplay dots :src="gallery"></q-gallery-carousel>
</div>
<!-- horizontal-quick-view -->

          <!-- <q-btn style="margin-left: 90%; width: 200px; height: 10px; margin-top: 5px;
            background-color: dark; background-color: #dddddd;" color="tertiary" @click="$refs.maximizedModal.close()">Close</q-btn> -->
     </q-modal>
        <!-- <div class="row items-center">
          <i aria-hidden="true" class="q-icon material-icons">view_carousel</i>
          <i aria-hidden="true" class="q-icon material-icons">fullscreen_exit</i>
        </div> -->
  </div>
  </div>

</template>

<script>

import { QSelect, QBtn, QInput, QModal, QModalLayout, QList, QItemMain, Ripple, QGallery, QGalleryCarousel, QIcon } from 'quasar'

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
    QIcon
  },
  props: {
    // documentType: {
    //   type: String,
    //   required: true
    // },
    // value: {
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
          label: 'Visualizar',
          ref: 'maximizedModal'
        }
        // {
        //   label: 'Foto',
        //   ref: ''
        // },
        // {
        //   label: 'Update de Foto',
        //   ref: ''
        // }
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
  }, // event change
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
    openSpecialPosition (position) {
      this.position = position;
      this.$nextTick(() => {
      this.$refs.positionModal.open();
      });
    }
  },
  computed: {
  }
}
</script>

<style>

</style>
