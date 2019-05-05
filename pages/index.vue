<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <h1>Nuxt.js + uppy example</h1>
      <v-btn id="select-files">upload</v-btn>
    </v-flex>
  </v-layout>
</template>

<script>
import Uppy from '@uppy/core'
import XHRUpload from '@uppy/xhr-upload'
import Dashboard from '@uppy/dashboard'
import Webcam from '@uppy/webcam'

export default {
  data() {
    return {
      uppyId: 'uppy-trigger'
    }
  },
  mounted() {
    const uppy = Uppy()
      .use(Dashboard, {
        trigger: '#select-files'
      })
      .use(Webcam, { target: Dashboard })
      .use(XHRUpload, { endpoint: 'https://api2.transloadit.com' })
    uppy.on('complete', result => {
      // eslint-disable-next-line no-console
      console.log(
        'Upload complete! We’ve uploaded these files:',
        result.successful
      )
    })
  }
}
</script>
