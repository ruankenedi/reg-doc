<template>
  <div class="layout-padding row justify-center">
    <div style="width: 500px; max-width: 90vw;">
      <p class="caption">Gallery</p>
      <q-gallery :src="gallery"></q-gallery>

    </div>
  </div>
</template>

<script>
import {
  QGallery,
  QGalleryCarousel
} from 'quasar'
export default {
  components: {
    QGallery,
    QGalleryCarousel
  },
  data () {
    return {
      gallery: [
         require('../assets/vue.png'),
         require('src/assets/js.png',),
         require('src/assets/react.png',),
         require('src/assets/npm.png',),
         require('src/assets/node.png',),
         require('src/assets/quasar-logo-full.svg')
      ] 
    }
  }
}
</script>