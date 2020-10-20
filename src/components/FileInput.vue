<template>
  <div>
    <div class="FileInput--text-input-wrapper">
      <input type="text" class="form-control" v-model="FileName" readonly>
    </div>
    <div class="FileInput--file-input-wrapper">
      <label class="custom-file-upload" :style="buttonStyle">
        <input
          class="file"
          type="file"
          ref="file"
          v-on:change="emitFileChange"
          v-show="false"
          :accept="acceptType"
        />
        {{placeholderButtonText}}
      </label>
    </div>
  </div>
</template>

<script>
import { defineComponent, ref, computed, onMounted } from 'vue'

export default defineComponent({
  name: 'FileInput',
  props: {
    isImage: {
      type: Boolean,
      default: false
    },
    isPdf: {
      type: Boolean,
      default: false
    },
    isWord: {
      type: Boolean,
      default: false
    },
    isExcel: {
      type: Boolean,
      default: false
    },
    isVideo: {
      type: Boolean,
      default: false
    },
    isAudio: {
      type: Boolean,
      default: false
    },
    buttonBackgroundColor: {
      type: String,
      default: () => '#003e70'
    },
    buttonTextColor: {
      type: String,
      default: () => '#FFF'
    },
    placeholderInputText: {
      type: String,
      default: () => 'Select a file'
    },
    placeholderButtonText: {
      type: String,
      default: () => 'Select a file'
    }
  },
  setup (props, context) {
    const file = ref(null)
    const FileName = ref(null)

    const acceptType = computed(() => {
      if (props.isExcel) {
        return '.xlsx, .xls'
      } else if (props.isWord) {
        return '.doc, .docx'
      } else if (props.isImage) {
        return 'image/*'
      } else if (props.isVideo) {
        return 'video/*'
      } else if (props.isPdf) {
        return 'application/pdf'
      } else if (props.isAudio) {
        return 'audio/*'
      } else {
        return '*'
      }
    })

    const buttonStyle = computed(() => {
      return `background-color: ${props.buttonBackgroundColor}; color: ${props.buttonTextColor};`
    })

    const emitFileChange = () => {
      if (file.value.files.length > 0) {
        const fileAux = file.value.files[0]
        FileName.value = fileAux.name
        const FileBlob = new Blob([file], {
          name: FileName.value,
          type: fileAux.type
        })
        const fileURL = URL.createObjectURL(FileBlob)
        const response = {
          file: file.value.files[0],
          fileName: file.value.files[0].name,
          fileBlob: fileURL,
          fileType: fileAux.type
        }

        context.emit('update:modelValue', response)
      } else {
        context.emit('update:modelValue', null)
        FileName.value = props.placeholderInputText
      }
    }

    onMounted(() => {
      FileName.value = props.placeholderInputText
    })

    return {
      FileName,
      acceptType,
      buttonStyle,
      emitFileChange,
      file
    }
  }
})
</script>

<style scoped>
.FileInput--text-input-wrapper {
  float: left;
  width: 60%;
}
.FileInput--text-input-wrapper > .form-control {
  background-color: white;
  width: 100%;
  display: block;
  height: 28px;
  border-width: 1px;
}
.FileInput--file-input-wrapper {
  float: left;
  width: 40%;
}
.FileInput--file-input-wrapper > .custom-file-upload {
  border: 1px solid #ccc;
  /* background-color: #003e70;
  color: #fff; */
  width: 100%;
  line-height: inherit;
  text-align: center;
  display: inline-block;
  padding: 6px 12px;
  cursor: pointer;
  transition: all ease .2s;
}
.FileInput--file-input-wrapper > .custom-file-upload > .file {
  display: none !important;
}
.file {
  display: none !important;
}
.FileInput--file-input-wrapper > .custom-file-upload::hover {
  background-color: lighten(#003e70, 5%);
  box-shadow: 0 14px 26px -12px rgba(156, 39, 176, 0.42), 0 4px 23px 0px rgba(0, 0, 0, 0.12), 0 8px 10px -5px rgba(156, 39, 176, 0.2);
}
@media(min-width: 768px) {
  .FileInput--text-input-wrapper {
    width: 70%;
  }
  .FileInput--file-input-wrapper {
    width: 30%;
  }
}
@media(min-width: 992px) {
  .FileInput--text-input-wrapper {
    width: 80%;
  }
  .FileInput--file-input-wrapper {
    width: 20%;
  }
}
</style>
