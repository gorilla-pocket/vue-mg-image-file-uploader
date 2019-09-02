# vue-mg-image-file-uploader
vue-mg-image-file-uploader

![npm](https://img.shields.io/npm/v/vue-mg-image-file-uploader)
![npm](https://img.shields.io/npm/dm/vue-mg-image-file-uploader)

## Installation

```
npm i vue-mg-image-file-uploader
```

## Usage

app.js

```javascript
import ImageFileUploader from 'vue-mg-image-file-uploader'
Vue.component('ImageFileUploader', ImageFileUploader)
```

Example:

```html
<template>
  <section class="container mt-2">
    <image-file-uploader :upload-files.sync="update_files"/>
  </section>
</template>

<script>
export default {
  data() {
    return {
      update_files: [],
    }
  },
  methods: {
    //
  },
}
</script>
```

## License

MIT
