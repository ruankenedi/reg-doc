<template>
  <div class="layout-padding docs-input row justify-center">
    <div style="display: flex;">
      <div style="display: flex; flex-wrap: wrap;">
        <q-field
          v-if="showSelect"
          style="min-width: 260px; margin-right: -20px;"
          :label-width="3"
          :icon="icons.description"
        >
          <q-select v-model="select" :options="selectOptions" @change="toggleDisplay" float-label="Document" />
        </q-field>

        <q-field
          style="margin-right: -20px; min-width: 260px;"
          :icon="icons.description"
          v-show="showInput"
          :label="label"
          :label-width="3"
        >
          <q-input
          ref="input1"
          @blur="blur"
          v-model="text"
          float-label="Other doc."/>
        </q-field>

        <q-field
          style="min-width: 260px; margin-right: 0px;"
          :label="label"
          :icon="icons.docNumber"
        >
          <q-input type="number" v-model="inputValue" @change="emitData()" float-label="Doc. Number"/>
        </q-field>

       <div>
        <q-btn color="primary" style="margin-top: 22px; margin-left: -95x;"
          link v-for="modal in optionsModal" :key="modal" flat @click="requestFullscreen" v-ripple.mat>
          <q-item-main :label="modal.label" @click="modalFull"/> <q-icon name="photo library" style="margin: 2px;"></q-icon>
        </q-btn>
      </div>

        <q-modal ref="maximizedModal" maximized :content-css="{padding: '0px'}">
          <div :style="{display: none}">
            <q-gallery-carousel @slide="emitData" ref="gallery" fullscreen infinite dots :src="gallery"></q-gallery-carousel>
          </div>
        </q-modal>
    </div>
    </div>
  </div>
</template>

<script>
import QGalleryCarousel from './GalleryCarousel.vue'
import { QField, QSelect, QBtn, QInput, QModal, QModalLayout, QList, QItemMain, Ripple, QGallery, QIcon } from 'quasar'

export default {
  name: 'sDocField',
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
  model: {
    prop: 'value',
    event: 'change'
  },
  props: {
    type: {
      type: [String, Array],
      default() {
        return '';
      },
      required: false
    },
    value: {
      type: Object,
    },
    showIcons: {
      type: Boolean,
      required: false,
      default: true
    },
    images: {
      type: Array,
      required: false
    }
  },
  directives: {
    Ripple
  },
  mounted() {
    this.iconsShow;
    this.labelShow;
    this.showSelecto;
  },
  data () {
    return {
      none: 'none',
      label: '',
      text: '',
      select: '',
      selectOptions:
      [
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
      optionsModal: [
        {
          ref: 'maximizedModal'
        },
        // {
        //   label: 'Foto',
        //   ref: ''
        // },
        // {
        //   label: 'Upload de Imagem',
        //   ref: ''
        // }
      ],
      // numberDocuments : [
      //   {
      //     label: 'CPF',
      //     number: '123'
      //   }
      // ],
      gallery: [
         require('src/assets/vue.png'),
         require('src/assets/js.png'),
         require('src/assets/react.png'),
         require('src/assets/npm.png'),
         require('src/assets/node.png'),
         require('src/assets/quasar-logo-full.svg'),
         require('src/assets/vue.png'),
         require('src/assets/js.png'),
         require('src/assets/react.png'),
         require('src/assets/npm.png'),
         require('src/assets/node.png'),
         require('src/assets/quasar-logo-full.svg')
      ],
      showInput: false,
      inputValue: '',
      showSelect: true,
      position: 'bottom',
      icons: {
        description: 'description',
        docNumber: 'description'
      }
    }
  },
  updated() {
    if (this.select === 'Other') {
      this.$refs.input1.focus();
    }
  },
  methods: {
    toggleDisplay(selected) {
      this.emitData();
      if (selected === 'Other') {
       this.showInput = true;
        this.showSelect = false;
        return;
      }
      this.showInput = false;
      this.showSelect = true;
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
        this.select = '';
        this.selectOptions.push({
          label: text,
          value: text
        });
      }
    },
    emitData() {
      this.$emit('change', {
        doc: this.select,
        num: this.inputValue,
        img: this.gallery
      })
    },
    typeArray() {
      this.selectOptions.splice(0, this.selectOptions.length);
      this.type.forEach((item, index, curr) => {
        this.selectOptions.push({
          label: item,
          value: item
        });
      });
      this.showSelect = true;
    }
  },
  computed: {
    labelShow() {
      if(!this.showSelect)
      {
        this.label = this.label;
      }
    },
    showSelected() {
      if(Array.isArray(this.$props.type)) {
        return;
      }
    },
    iconsShow() {
      if (Array.isArray(this.type)) {
        this.icons.docNumber = '  ';
        this.label = '';
        this.typeArray();
        return;

      } else if (typeof this.type === 'string') {
        this.icons.docNumber = 'description';
        this.label = this.type;
        this.showSelect = false;
      }
      if (this.type === '') {
        this.icons.docNumber = '  ';
        this.showSelect = true;
      }
    }
  }
}
</script>

<style>

</style>
