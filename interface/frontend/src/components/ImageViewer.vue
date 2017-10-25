<template>
<div>
  <button @click="loadImage()">load dicom image</button>
  <div id="dicom-image" style="width:512px;height:512px;"></div>
</div>
</template>

<script>
import * as cornerstone from 'cornerstone-core'
import { loadDummyDicomImages } from '../util/data'
import $ from 'jquery'

export default {
  created () {
    cornerstone.external.$ = $
  },
  data () {
    return {
      showImage: false
    }
  },
  methods: {
    loadImage () {
      this.showImage = !this.showImage
      loadDummyDicomImages(cornerstone)
      let dicomImageElement = document.getElementById('dicom-image')
      cornerstone.enable(dicomImageElement)
      cornerstone.loadImage('example://1').then((image) => {
        cornerstone.displayImage(dicomImageElement, image)
      })
    }
  }
}
</script>
