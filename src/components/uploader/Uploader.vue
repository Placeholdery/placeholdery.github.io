<template>
  <div v-if="!Object.keys(files).length && !Object.keys(previewSize).length" class="uploader">
    <div>
      <image-icon size="10x" />
    </div>
    <div>
      <h2>Drag & Drop Image/s</h2>
      <p>or</p>
      <input @change="fileUpload" class="fileinput" type="file" multiple ref="fileinput" />
      <button @click="upload">Upload</button>
    </div>
  </div>
</template>

<script>
import { ImageIcon } from "vue-feather-icons";
export default {
  props: ["files", "previewSize", "fileUpload"],
  methods: {
    upload: function() {
      const fileInput = this.$refs["fileinput"];
      fileInput.click();
    }
  },
  components: {
    ImageIcon
  }
};
</script>