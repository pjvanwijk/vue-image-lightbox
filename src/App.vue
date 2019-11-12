<template>
  <div id="app" style="background-color: yellow" class="row">
    <div>
      <ul>
        <li 
          v-for="(image, index) in images" 
          style="display: inline-block"
        >
          <img 
            v-lazy="image.src" 
            style="height: 100px" 
            @click="openGallery(index)"
          >
        </li>
      </ul>
      <LightBox 
        :images="images" 
        ref="lightbox"
        :show-caption="true"
        :show-light-box="false"
        :has-overlay="true"
      >
        <template v-slot:overlay="overlayProps">
          <div v-html="overlayProps.caption ? overlayProps.caption : '<h1>untitled image<h1>'"></div>
          <p>{{ overlayProps.details ? overlayProps.details.description : ""}}</p>
          <a :href="overlayProps.imagesrc">Download this image</a>
        </template>
      </LightBox>
    </div>
  </div>
</template>

<script>
import LightBox from 'components/LightBox'

import siteLoading from './siteloading.gif'
import images from './dummy'

export default {
  components: {
    LightBox,
  },

  data () {
    return {
      images,
      siteLoading,
    }
  },

  methods: {
    openGallery(index) {
      this.$refs.lightbox.showImage(index)
    }
  }
}
</script>
