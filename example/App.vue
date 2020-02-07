<template>
  <section class="container mt-2">
    <image-file-uploader :upload_files.sync="update_files">
    <!-- <button class="btn" @click="onClick">テスト</button> -->
      <template v-slot:button-display>
        <i class="fas fa-plus"></i>テスト
      </template>
    </image-file-uploader>
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
    onClick: function () {
      this.update_files.push({
        id: null,
      })
    }
  },
  components: {
    ImageFileUploader,
  },  
}
</script>

<style scoped>
@import 'https://use.fontawesome.com/releases/v5.7.2/css/all.css';
</style>