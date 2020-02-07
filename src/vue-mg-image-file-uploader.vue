<template>
<div class="vue-mg-image-file-uploader">
    <div>
        <input type="file" name="files[]" v-bind="attr" style="display:none" @change="onFileChange" ref="file" :accept="accept"/>
        <div>
            <button type="button" class="btn btn-primary" @click="$refs.file.click()">
                <slot name="button-display">
                    <i class="fas fa-plus"></i> ファイル
                </slot>
            </button>
        </div>
    </div>
    <div class="d-flex align-content-start flex-wrap mt-2">
        <div class="image-container mr-2 mb-2" v-for="(upload_file, index) in wk_upload_files" :key="index" v-show="upload_file.image">
            <img
                class="preview-item-file"
                :src="upload_file.image"
                :style="'height:'+image_size"
                alt=""
            />
            <button type="button" class="btn btn-sm btn-danger btn-delete ml-2" @click="onDelete(index)"><i class="fas fa-times"></i></button>
        </div>
    </div>
</div>
</template>
<script>
export default {
    props: {
        upload_files: {
            default: function () {
                return []
            },
        },
        image_size: {
            default: '110px',
        },
        is_multiple: {
            default: true,
        },
        accept: {
            default: '.jpg,.gif,.png,image/gif,image/jpeg,image/png',
        }
    },
    data: function() {
        return {
            wk_upload_files: [],
            uploadedImage: '',
            img_name: '',
        }
    },
    mounted: function () {
        this.wk_upload_files = this.upload_files
    },
    watch: {
        upload_files: function (val) {
            this.wk_upload_files = val
        },
    },
    computed: {
        attr: function () {
            if (this.is_multiple) {
                return {
                    multiple: 'multiple'
                }
            } else {
                return ''
            }
        }
    },
    methods: {
        onFileChange: function (e) {
            const files = e.target.files || e.dataTransfer.files
            for( let i = 0 ; i < files.length ; i++){
                this.createImage(files[i], files[i].name)
            }
        },
        createImage(file, file_name) {
            const reader = new FileReader()
            reader.onload = e => {
                this.wk_upload_files.push({
                    id: null,
                    image: e.target.result,
                    file_name: file_name,
                })
                this.$emit('update:upload_files', this.wk_upload_files)
            };
            reader.readAsDataURL(file)
        },
        onDelete: function (index) {
            const upload_file = this.wk_upload_files[index]
            if (upload_file.id) {
                upload_file.is_dirty = true
                upload_file.image = ''
            } else {
                this.wk_upload_files.splice(index, 1)
            }
        }
    },
}
</script>
<style scoped>
.image-container {
    position: relative;
}
.btn-delete {
    position: absolute;
    top: 0;
    right: 0;
    opacity: .7;
}
.btn-delete:hover {
    opacity: 1;
}
</style>