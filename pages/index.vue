<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <center>
        <h1>Nuxt.js + uppy example</h1>
        <v-btn id="select-files" color="primary">upload</v-btn>
      </center>
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
      .use(Webcam, { target: Dashboard }) // ウェブカメラを追加
      .use(XHRUpload, { endpoint: 'https://api2.transloadit.com' }) // ダミーのURLへアップロード
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
