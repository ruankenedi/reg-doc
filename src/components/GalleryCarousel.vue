<template>
  <q-carousel
      ref="slider"
    @slide="__updateCurrentSlide"
    :dots="dots"
    :arrows="arrows"
    :fullscreen="fullscreen"
    :infinite="infinite"
    actions
    :animation="animation"
    :autoplay="autoplay"
    class="text-white bg-black q-gallery-carousel"
  >
    <div
      v-for="(img, index) in src"
      :key="index"
      :ref="index"
      slot="slide"
      class="no-padding row flex-center"
    >
      <div class="full-width">
        <img :src="img">
      </div>
    </div>

    <div
      class="q-gallery-carousel-overlay"
      :class="{active: quickView}"
      @click="toggleQuickView()">
    </div>


    <q-icon name="view_carousel" slot="action" @click="toggleQuickView()"/>
    <q-icon name="delete" slot="action" @click="exclude()"/>
    <q-icon name="file upload" slot="action"/>
    <q-icon name="add a photo" slot="action"/>

    <div
      class="q-gallery-carousel-quickview"
      :class="{active: quickView, row: horizontalQuickView, horizontal: horizontalQuickView}"
      @touchstart.capture.stop
      @touchmove.capture.stop
      @touchend.capture.stop
      @mousedown.capture.stop
      @mousemove.capture.stop
      @mouseend.capture.stop
    >
      <div v-for="(img, index) in src" :key="index">
        <img
          :src="img"
          :class="{active: currentSlide === index}"
          @click="__selectImage(index)"
        >
      </div>
    </div>
  </q-carousel>
</template>

<script>
import { QCarousel, QIcon, Dialog, Toast } from 'quasar'
import CarouselMixin from './carousel-mixin'

export default {
  name: 'q-gallery-carousel',
  components: {
    QCarousel,
    CarouselMixin,
    QIcon
  },
   mixins: [CarouselMixin],
  props: {
    src: {
      type: Array,
      required: true
    },
    arrows: {
      type: Boolean,
      default: true
    },
    actions: {
      type: Boolean,
      default: true
    },
    horizontalQuickView: Boolean
  },
  data () {
    return {
      quickView: false,
      currentSlide: 0
    }
  },
  methods: {
    openDialog() {
      const self = this;
      Dialog.create({
        title: 'Confirm',
        message: 'Deseja realmente excluir essa imagem ?',
        buttons: [
          {
            label: 'Disagree',
            handler () {
              if ('Disagreed') {
                 const i = self.src.indexOf(self.currentSlide);
                 self.$refs.slider.toggleFullscreen();
              }

            }
          },
          {
            label: 'Agree',
            handler () {
              if ('Agreed') {
                const i = self.src.indexOf(self.currentSlide);
                self.src.splice(self.currentSlide, 1);
                self.$refs.slider.toggleFullscreen();
              }
            }
          }
        ]
      });
    },
    toggleQuickView () {
      this.quickView = !this.quickView;
    },
    goToSlide (index, noAnimation) {
      this.$refs.slider.goToSlide(index, noAnimation);
    },
    __selectImage (index) {
      this.goToSlide(index, true);
      this.toggleQuickView();
    },
    __updateCurrentSlide (value) {
      this.currentSlide = value;
      this.$emit('slide', value);
    },
    numberImg() {
       if (this.src.length === 0) {
        const i = this.src.indexOf(this.currentSlide);
        this.$refs.slider.toggleFullscreen();
      }
    },
    exclude () {
      this.numberImg();
      this.openDialog();
    }
  }
}
</script>
<style>
  .modal {
    z-index: 30000;
  }
</style>
