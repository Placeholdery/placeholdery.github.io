<template>
  <Layout>
    <div v-if="!files.length" class="uploader">
      <div>
        <image-icon size="10x" />
      </div>
      <div>
        <h2>Drag & Drop Image/s</h2>
        <p>or</p>
        <input
          @change="fileUpload"
          class="fileinput"
          type="file"
          multiple
          ref="fileinput"
        />
        <button @click="upload">Upload</button>
      </div>
    </div>
    <div v-else class="upload-action">
      Action
    </div>
  </Layout>
</template>

<style>
.fileinput {
  display: none;
}
</style>

<script>
import { ImageIcon } from "vue-feather-icons";

export default {
  metaInfo: {
    title: "Homepage"
  },
  data: () => {
    return {
      files: []
    };
  },
  methods: {
    upload: function() {
      const fileInput = this.$refs["fileinput"];
      fileInput.click();
    },
    fileUpload: function(e) {
      const {
        target: { files }
      } = e;
      if (files.length) {
        this.files = files;
      }
    }
  },
  components: {
    ImageIcon
  }
};
</script>

<style>
.uploader {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
}
</style>
