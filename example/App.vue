<template>
  <section class="container mt-2">
    <image-file-uploader :upload-files.sync="update_files"/>
  </section>
</template>

<script>
import ImageFileUploader from '../src/vue-mg-image-file-uploader'
import 'bootstrap/dist/css/bootstrap.min.css'
export default {
  data() {
    return {
      update_files: [],

      isLoading: false,
    }
  },
  methods: {
    //
  },
  components: {
    ImageFileUploader,
  },  
}
</script>

<style scoped>
@import 'https://use.fontawesome.com/releases/v5.7.2/css/all.css';
</style>