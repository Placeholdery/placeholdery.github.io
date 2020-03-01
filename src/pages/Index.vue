<template>
  <Layout>
    <div class="uploader">
      <div>
        <image-icon size="10x" />
      </div>
      <div>
        <h2>Drag & Drop Image/s</h2>
        <p>or</p>
        <input class="fileinput" type="file" multiple ref="fileinput" />
        <button @click="upload">Upload</button>
      </div>
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
